1. OpenSearchConfig에서 빈 등록

@Slf4j
@Configuration
public class OpenSearchConfig {
    @Value("${opensearch.protocol}")
    private String protocol;
    @Value("${opensearch.host}")
    private String host;
    @Value("${opensearch.port}")
    private Integer port;
    @Value("${opensearch.id}")
    private String id;
    @Value("${opensearch.pw}")
    private String pw;
    @Value("${opensearch.useAuth}")
    private boolean useAuth;
    @Value("${opensearch.connConfig.conTimeout}")
    private Integer conTimeout;
    @Value("${opensearch.connConfig.socketTimeout}")
    private Integer socketTimeout;
    @Value("${opensearch.connConfig.keepAlive}")
    private Integer keepAlive;
    @Value("${opensearch.connConfig.conReuse}")
    private boolean conReuse;

    @Bean(name = "osHighClient")
    public RestHighLevelClient createOpenSearchRestClient() throws NoSuchAlgorithmException, KeyManagementException, KeyStoreException {
        final CredentialsProvider credentialsProvider = new BasicCredentialsProvider();

        if (useAuth)
            credentialsProvider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(id, pw));

        SSLContext sslcontext = SSLContext.getInstance("TLS");
        sslcontext.init(
                null, new TrustManager[]{
                        new X509TrustManager() {
                            public void checkClientTrusted(X509Certificate[] arg0, String arg1) throws CertificateException {
                            }

                            public void checkServerTrusted(X509Certificate[] arg0, String arg1) throws CertificateException {
                            }

                            public X509Certificate[] getAcceptedIssuers() {
                                return new X509Certificate[0];
                            }
                        }
                }
                , new java.security.SecureRandom()
        );

        TrustStrategy acceptingTrustStrategy = new TrustSelfSignedStrategy();
        SSLContext sslContext = org.apache.http.ssl.SSLContexts.custom().loadTrustMaterial(null, acceptingTrustStrategy).build();

        RestClientBuilder builder = RestClient.builder(new HttpHost(host, port, protocol))
                .setRequestConfigCallback(
                        requestConfigBuilder -> requestConfigBuilder
                                .setConnectTimeout(conTimeout)
                                .setSocketTimeout(socketTimeout))
                .setHttpClientConfigCallback(new RestClientBuilder.HttpClientConfigCallback() {
                    @Override
                    public HttpAsyncClientBuilder customizeHttpClient(HttpAsyncClientBuilder httpClientBuilder) {
                        return httpClientBuilder
                                .setDefaultCredentialsProvider(credentialsProvider)
                                .setConnectionReuseStrategy((response, context) -> conReuse)
                                .setKeepAliveStrategy(((response, context) -> keepAlive))
                                .setSSLContext(sslContext)  //ssl인증서 오류로 인해 추가
                                .setSSLHostnameVerifier(new NoopHostnameVerifier());
                    }
                });
        return new RestHighLevelClient(builder);
    }

    //////////////////////////////////////////////////////////////////////////////////////////
    // Initializing the client with SSL and TLS enabled using RestClient Transport
    // Opensearch java client 신규 API용.
    //////////////////////////////////////////////////////////////////////////////////////////
    @Bean(name = "osClient")
    public OpenSearchClient openSearchClientWithRestClient() {
      final HttpHost httpHost = new HttpHost(host, port, protocol);

      final CredentialsProvider credentialsProvider = new BasicCredentialsProvider();
      // 내 로컬에서는 os username, password 설정 없음
      if (useAuth) {
        credentialsProvider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(id, pw));
      }

      // SSL 인증서를 무시하는 SSLContext를 생성
      SSLContext sslContext = null;
      try {
        sslContext = SSLContexts.custom().loadTrustMaterial(new TrustSelfSignedStrategy()).build();
      } catch (Exception e) {
        // SSLContext 생성에 실패한 경우 예외 처리
        e.printStackTrace();
      }

      // SSLContext를 사용하여 SSL 인증서를 무시하도록 설정
      if (sslContext != null) {
        SSLContext finalSslContext = sslContext;
        final RestClient restClient = RestClient.builder(httpHost)
            .setHttpClientConfigCallback(httpClientBuilder -> httpClientBuilder
                .setDefaultCredentialsProvider(credentialsProvider)
                .setSSLContext(finalSslContext)
                .setSSLHostnameVerifier(NoopHostnameVerifier.INSTANCE))
            .build();

        final OpenSearchTransport transport = new RestClientTransport(restClient,
            new JacksonJsonpMapper());
        return new OpenSearchClient(transport);
      }

      return null; // SSLContext 생성에 실패한 경우 null 반환하거나 예외 처리를 진행할 수 있습니다.
    }
}


2. 사용하는곳(OsNewApiAggregationService) 에서 주입받음
@Slf4j
@Service
public class OsNewApiAggregationService {
  private final OpenSearchClient client;

  @Autowired
  public OsNewApiAggregationService(@Qualifier("osClient") OpenSearchClient client) {
    this.client = client;
  }
































