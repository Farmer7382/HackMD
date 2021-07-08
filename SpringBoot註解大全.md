# Spring Boot註解大全

#### @SpringBootApplication
> 建立Spring Boot啟動器

> 等於@SpringBootConfiguration + @EnableAutoConfiguration + @ComponentScan

> @SpringBootApplication(scanBasePackages = {"com.my.package.controller"})  //與底下用法相同，但底下用法較為穩定
 
> @ComponentScan({"com.my.package.controller"})
>

#### @SpringBootConfiguration
> 標註當前類是配置類

#### @EnableAutoConfiguration
> Springboot根據你新增的jar包來配置你專案的預設配置

#### @Configuration
> @Configuration的作用同以前的xml配置檔，用來設定Spring環境配置，例如宣告及註冊bean至Spring容器中，注入properties參數等。

> @Configuration = @SpringBootConfiguration

> @SpringBootApplication類本身即包含了@Configuration

#### @ComponentScan
> @ComponentScan的目的是透過掃描package去檢查有什麼class會被註冊為Spring的bean。

> @ComponentScan會掃描包含以下注解的class:
@Component  @Service  @Controller  @RestController  @Repository  @Configuration

#### @Controller
> 用於Controller class開頭註解

#### @Service
> 用於Service class開頭註解

#### @Repository
> 用於Repository class開頭註解

#### @ResponseBody
> 將返回值轉為JSON數據

#### @RestController
> 等於@ResponseBody + @Controller 的註解

#### @Component
> @Component是Spring中的一个註解，它的作用就是實現bean的注入

> 當你的一個類被@Component所註解，那麼就意味著同樣可以用@Repository, @Service, @Controller來替代它，同時這些註解會具備有更多的功能，而且功能各異。

#### @RequestMapping
> @RequestMapping("/demo3") //打在URL的請求

> 沒有寫method的話，默認GET、POST都可以訪問的到。

> @RequestMapping(value = "/loading", method = RequestMethod.POST, consumes = { "application/x-www-form-urlencoded" })

#### @GetMapping
> @GetMapping = @RequestMapping(method = RequestMethod.GET)

> @GetMapping的位置只能在class之內，而@RequestMapping在內外也可以。

#### @PostMapping
> @PostMapping = @RequestMapping(method = RequestMethod.POST)

> @PostMapping(value = "/RIAF021PLoad")

#### @RequestParam
> 註解@RequestParam接收的參數是來自requestHeader中，即請求頭。通常用於GET請求，像POST、DELETE等其它類型的請求也可以使用。

> 放在方法後(@RequestParam XXX)接收外來傳入參數，不可為集合等參數。EX:Postman Request



#### @RequestBody
> 註解@RequestBody接收的參數是來自requestBody中，即請求體。一般用於處理非 Content-Type: application/x-www-form-urlencoded編碼格式的數據，比如：application/json、application/xml等類型的數據。通常用於接收POST、DELETE等類型的請求數據，GET類型也可以適用。

> 放在方法後(@RequestBody XXX)接收外來傳入參數，可為集合等參數。EX:Postman Request

#### @Autowired
> 可以對類成員變數、方法及建構函式進行標註，完成自動裝配的工作。

> 用來抓取bean xml的配置資料

#### @Bean
> 註解在方法上，聲明當前方法返回一個Bean

#### @Lazy
> 在沒有此註解時，單例Bean會在容器初始化時即創建。使用此註解後，單例Bean會在第一次使用時創建，並且只創建一次。

> 只對單例Bean有用，原型Bean對此註解不起作用。

#### @CrossOrigin
> 實現跨網域請求。

#### @WebServlet
> @WebServlet:聲明該類為Servlet程序

>@WebServlet(name="helloServlet",urlPatterns="/helloServlet")等同於web.xml配置
#### @WebFilter
> 過濾器
@WebFilter(filterName="helloFilter",urlPatterns="/helloServlet") //urlPatterns=攔截路徑
public class HelloFilter implements Filter{

#### @WebListener
> 監聽器
@WebListener
public class HelloListener implements ServletContextListener{

#### @ServletComponentScan
> 使用@ServletComponentScan註解(會去掃描@WebServlet、@WebFilter、@WebListener等註解) 

> 寫在啟動器上

#### @SuppressWarnings
> 指示編譯器去忽略註解中聲明的警告




#### @Api

#### @ApiOperation

#### @ApiResponses

#### @Scope

#### @Value

#### @Entity




Postman: 可沒有值，但KEY一定要寫下去
