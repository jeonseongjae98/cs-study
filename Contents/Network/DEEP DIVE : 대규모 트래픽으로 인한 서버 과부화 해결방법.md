## 대규모트래픽 처리의 중요성

웹 서비스를 다루는데있어 트래픽을 처리하는 구조를 설계하고 적용하는 것은 개발자의 필수 역량이다.  
특히 서비스의 규모가 커질수록 개발자가 의도한 대로 프로그램이 작동하지않는 경우가 발생한다.  
아무리 뛰어난 성능을 가진 서버라고해도 모든 트래픽을 감당할수는 없으므로 서비스의 안정적인 구동과 만족도높은 고객경험을 제공하기위해 대용량 트래픽을 다루는기술을 학습하고 대비해야한다.  
> ex} 네이버페이, 토스페이, 카카오페이 처럼 경쟁사가 많을수록 서버가 한번터져서 사용자의 요청을 제대로소화해내지 못하면 사용자가 불쾌함과 불편함을 느끼게되고 
사용자가 영구히 이탈해버린다면 큰 손실이 발생한다. 


## 서버가 터지는 이유  
결국 서버도 외부로부터 요청을 받아 처리해주고 응답을 주는 프로그램이 돌아가는 컴퓨터이기때문에 처리속도와 한계가 CPU, 메모리, 저장장치에 영향을 받는다.
사용자가 많아질수록 서버에는 많은 HTTP request가 발생하고 request가 많아졌다는것은 트래픽이 높아졌다는 의미이다.  
Request는 Queue를 통하여 Thread pool에 할당하게되는데 Thread pool size를 초과하는 요청은 큐에서 대기한다. Thread의 개수는 무한하지 않으므로 시스템에 할당된 성능에따라 제한된다.  
따라서 Thread pool size를 초과하는 대량의 트래픽이 지속적으로 발생하면 서버의 지연시간은 기하급수적으로 증가하게된다. 이와같은 현상을 Thread pool hell이라고 한다.

![image](https://github.com/NoRuTnT/practice/assets/114069644/5beb2553-302e-406d-a354-0628cac2a5f1)  

### 큐 오버플로우  
아래는 Tomcat의 요청 수락/처리와 관련된 그림이다.
> ![image](https://github.com/NoRuTnT/practice/assets/114069644/4a49195a-5ecd-4836-bde5-85625a6a3dd2)  
> maxThreads : 동시에 일하는 스레드의 최대 개수이다.  
> maxConnections : 하나의 Tomcat 인스턴스가 동시에 유지할 수 있는 Connection의 최대 개수이다.  
> acceptCount : maxConnections를 초과하는 요청에 대한 대기큐의 크기이다.

maxThreads는 일하는 놈이 몇이나 있는가  
maxConnections는 받아서 처리를 할 예정이지만 아직 처리되지 않은 요청들의 큐( Keep Alive를 통해 일부러 연결을 유지시킨 요청도 포함)  
acceptCount는 maxConnection의 개수를 넘어가는 추가 요청들을 몇 개까지 가지고 있을것인가..  

### 타임아웃
요청에는 대개 타임아웃이 설정되어 있다. 보낸 요청이 처리될 때까지 언제까지고 기다릴 수는 없으므로 일정 시간이 지나면 실패로 간주해버리는 것인데, 서버가 다른 요청들을 처리하느라고 바빠서 그 이후에 들어온 요청들을 타임아웃이 걸릴 때까지 처리하지 못 할 경우, 사용자 입장에서는 역시 서버가 터졌나 싶은 응답을 받게 된다.  

## 서버리소스부족 해결방안
서버가 터지는 이유는 결국 아직 처리되지 못한 요청이 쌓이고 쌓이고 쌓여서 그렇게 되는 것이므로, 단순히 생각해 요청을 충분히 빠르게 처리하면 된다.  
서버 리소스부족문제는 보통 2가지 방법으로 해결책이 나뉜다.

### (vertical) scale-up
Scale Up 방식은 말그대로 고성능 CPU, 메모리 확장, SSD 등 서버의 스펙을 높이는 수직 확장 방식.
그중에서도 중요한것은 기억장치의 처리속도이다. 예외로 머신러닝같은 모델트레이닝같은경우는 어마어마한양의 연산이 들어가서 cpu가 중요할수도있지만 해당작업은 특별한서비스가아닌이상 드물고 대규모트래픽과는 별 연관이없다.  
그렇기때문에 대규모 트래픽 처리를 위한 scale-up을 고려하는 경우 기억장치의 처리 속도 업그레이드를 고려해야 한다.

### (horizontal) scale out
Scale out 방식은 여러대의 서버를 구축하여 서버 한대가 처리하는 용량을 줄임으로서 전체적인성능을 중가시키는 방법이다.  
한대가 부담해야했던 서버장애 리스크를 줄일수있고 가성비적인측면에서도 비교우위에있어 scale up보다 효율적인 리소스 부족 해결방식이다.  
모든요청이 동일한 처리 시간을 요구하지는 않기 때문에 어떤 요청은 보다 많은 처리 시간이 필요하고, 어떤 요청은 그렇지 않을 것이다.  
이때, 특정 서버에 장시간의 처리가 필요한 요청이 쏠리면 해당 서버만 터지게 될 것이고, 운 없게도 해당 서버로 요청을 보내게 된 사용자들은 불편하고 불쾌한 경험을 하게 될 것이다.  
이런 문제를 해결하기 위한 기술이 로드밸런싱이다.  

## 로드밸런싱
분산시스템을 구축한다고했을때 중요해지는것은 로드밸런싱이다.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/8be0886d-1c38-4d38-a712-f6cc14eaf21c)  
서버를 여러대를 가지고있으니까 들어오는 트래픽을 누구에게보낼지 분산시켜줄 모듈이 필요한데 그것을 로드밸런서라고 부른다.  

### 로드밸런서의 분산전략
#### Round Robin  
여러대의 서버가있을때 들어오는 리퀘스트를 서버에 순차적으로 나누어준다(Like 수건돌리기)  
이런방식은 트래픽을 모든서버가 골고루 분산해서 가져갈수있는 간단한 알고리즘  
![image](https://github.com/NoRuTnT/practice/assets/114069644/a7e47b9f-8f83-4700-abc8-fbaa604e76bf)  

#### Random Select
리퀘스트가들어왔을때 그냥 아무서버를 찍어서 그서버에 리퀘스트를 보내는방식.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/81b5e23c-c1aa-4b54-8b72-f312fea9d852)  

#### SMART - Least Connection
서버가 내가 얼마만큼의 트래픽을 감당하고 있고 얼마만큼의 커넥션을 맺고있는지 역으로 알려준다.  
로드 밸런서입장에서 이정보들을 가지고 판단을 한다. Adaptive하게 판단  
![image](https://github.com/NoRuTnT/practice/assets/114069644/38b4d3a2-a966-428a-8db2-a1d329c78665)  

#### SMART - Ratio
모든서버들의 스펙이 같지않은경우 성능차이를 고려하지않고 트래픽을 주게되면 성능이낮은서버가 감당하지못해서 죽어버리면 다른서버에 부하가 커지게되고 연쇄적으로 서버가 다운될수있다. 이런부분을 고려하여 Ratio를 미리 부여하여 로드밸런싱.  
이때문에 모든서버스펙을 동일하게 맞추어놓는게 시스템 엔지니어입장에서는 고민할거리를 많이줄여준다.
![image](https://github.com/NoRuTnT/practice/assets/114069644/1e806d24-70cf-4c39-bc31-4ac1692ba48d)   

### 로드밸런서가 다운되었을때  
특정포인트에서 다운되었을때 전체시스템이 다운되는 경우를 SPOF라고 한다.  
로드밸런서를 한서버에서만 구축을해서 서비스하게되면 로트밸런서만죽으면 모든서비스가 다운되어버린다.  
따라서 로드밸런서자체도 스케일아웃을 할필요가있다.  
ex) 하나만 사용하는게아니라 마스터슬레이브방식으로 마스터가항상일을하되 마스터가 다운되어버리면 슬레이브를 마스터로임명시켜서 서비스를이어나갈수있게 구축  
![image](https://github.com/NoRuTnT/practice/assets/114069644/ccb93a47-ef4a-421f-8c0d-3d3108e1a058)  

### Scale out 정합성 문제
Scaleout 을 선택했을때 유저의 정보를 Session으로 저장하는것으로 설계했는데 정합성의 문제점이 발생할수있다.  
클라이언트의 Request들을 로드밸런서가 라운드로빈 방식으로 적절하게 관리했다고 가정했을때.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/ee009200-d222-4610-9c87-45ca6a2a0d77)   
여기서 A클라이언트가 Request를 보내면 LoadBalancer가 라운드로빈 방식으로 분배를 해주고 이때 A유저가 로그인 요청을 보내면 A Server에 A 유저의 정보를 Session으로 저장한다.  
그 다음에  A 유저가 자신의 정보를 호출하는 Request를 보내면 Load Balancer에서는 C Server로 전달하기 때문에 A 유저의 정보가 없어서 에러페이지가 뜨게 된다.  
#### Sticky Session
직역을 하면 고정된 세션이라는 뜻으로 A 유저의 모든 서비스 활동을 A Server에서 고정되어 사용하는 방법이다.
> 장점  
> 특정 세션의 요청을 처음 처리한 서버로만 보내기 때문에 정합성 이슈를 해결할 수 있다.
> 
> 단점  
> 특정서버에만 트래픽이 몰릴수가 있고 A Server가 다운되면 저장된 Session이 유실될 수 있다.  

#### Session Clustring
여러 대의 컴퓨터들이 하나의 시스템처럼 동작하도록 만드는 것을 클러스트링이라고 한다.  
A 클라이언트의 세션정보를 복사하여 A/B/C Server에 저장한다.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/ddf9556a-748e-49b2-9897-5763f16a5983)  
> 장점  
> 서버 한대가 시스템장애가 발생해도 다른 서버에서 그 역할을 대신 수행할 수 있다.  
> 위 그림처럼 A 클라이언트가 어떤 서버에 접속하더라도 정합성 이슈가 해결된다.
> 
> 단점  
> 모든 서버가 동일한 세션 객체를 가져야 하기 때문에 많은 메모리가 필요하다.  
> 서버 증설에 따라 모든 서버에 세션을 저장해야하기 때문에 트래픽이 증가할 수 있다.  

#### Session Storage
Session Storage는 별도의 세션 저장소를 이용하는 방법이다.  
데이터스토리지의 메인 메모리에 설치되어 운영되는 방식의 Inmemory DB를 사용한다.  
Inmemory DB의 장점은 메모리로 접근하기 때문에 디스크 접근보다 속도가 빠르고 내부 최적화 알고리즘을 사용하여 더 적은 CPU 명령을 실행한다.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/407d1ad8-2748-4079-aa30-d7bb67efedfe)  
> 장점  
> 세션 스토리지를 분리함으로서 세션의 정합성을 유지할 수 있다.   
> 서버 한대가 장애가 발생하더라도 별도의 세션 저장소가 존재하기 때문에 서비스를 계속해서 제공하여 가용성을 확보할 수 있다.  
> 
> 단점  
> 메모리 자체가 휘발성이기 때문에 DB 서버가 종료되면 Session 손실의 위험이 있다.  
> 네트워크 통신 기회비용이 발생할 수 있습니다.  

## 대용량트래픽 처리방법  
대용량 트래픽을 처리하는 방법은 어플리케이션의 구조와 설계방식, 시스템환경에따라 고정적이지 않고 다양한 방식을 적용할수있다.

### 1. scale out 적용/ In-memory DB 사용 세션일관성 유지
디스크가아닌 외부메모리에 데이터를 저장하는 데이터베이스를 In-memory DB라고한다. 디스크가아닌 메모리에 저장하기때문에 세션정보와 같은 임시데이터를 저장하는것이 바람직하다.(비용이 비쌈)  
서버들이 동일한 인메모리 데이터베이스를 바라보기때문에 서버추가가 용이하며 속도도빠른 Redis, Memchached와 같은 인메모리 데이터베이스를 사용해 일관성을 유지하는것을 고려해 볼만하다.  
<details>
   <summary>Redis vs Memcached</summary>
	<div>
		
    Redis는 NoSql이면서 많은 사람들이 사용하는 대표적인 인메모리DB이기 때문에 NoSQL 과 In-Memory-DB를 동의어로 생각한다.
   Redis의 장점
  1. CollectionAPI를 제공하기 때문에 리스트, 배열과 같은 데이터를 처리하는데 유용하다.
  2. 여러 프로세스에서 동시에 같은 key에 대한 갱신을 요청할 경우, Atomic 처리로 데이터 부정합 방지 Atomic처리 함수를 제공한다.
   3. 메모리를 활용하면서 영속적인 데이터 보존
   4. Redis Server는 1개의 싱글 쓰레드로 수행되며, 따라서 서버 하나에 여러개의 서버를 띄우는 것이 가능하다. Master - Slave 형식으로 구성이 가능함  
  Memcached  
   Memcached는 기본적으로 Redis와 매우 흡사하다. 그렇다면 어떤 부분이 다를까? 기본적으로 Memcached는 캐쉬솔루션이며 여기서 저장소가 추가된게 Redis이다. 캐시는 빠른 속도를 위해서 어떤 결과를 저장해 두는 것을 의미하며 또한 데이터가 사라지면 다시 만들 수 있다는 전제를 내포하고 있다.
캐시 기능만을 고려한다면 디스크에서 불러오기만 하면 된다. (= Load 기능만 수행되면 된다.) 
  그런데 저장소라는 개념이 추가되면 데이터가 유지되어야 한다는 특성을 가지게 된다.(= Save기능도 필요하다.)
  ![image](https://github.com/NoRuTnT/practice/assets/114069644/3b79ef01-d9b6-4fc8-9d95-52ed6db08bf3)
</div>
</details>

### 2. 캐싱을 통한 DB부하분담
서비스에서 공통된 데이터를 지속적으로 사용자에게 제공하는 경우가 있다. 사용자에게 필요한 공통된 정보를 제공하기 위해 매번 DB 에 접근해 데이터를 조회하는 것은 데이터 베이스 서버의 리소스를 낭비하는 것이며 서버 전체 성능에도 악영향을 줄 수 있다. 이때 자주 사용 되는 데이터를 임시로 캐시 서버에 저장해 제공하는 방법을 고려해야 한다. 캐시는 로컬캐시(Local Cache) 와 글로벌캐시(Globa Cache)로 구분되는데 Spring MSA 방식에서는 글로벌 캐시를 통해 다중 서버에서 동일한 데이터를 전달 받을 수 있도록 Redis를 적용할 수 있다.   
![image](https://github.com/NoRuTnT/practice/assets/114069644/b0b87b1e-a748-4875-9601-d8ce5380f14f)  
Spring 에서 Redis 인메모리 캐싱을 활용하기 위한 간단한 예제 코드  

```
@EnableCaching // CacheManager 인터페이스를 구현한 Bean 등록
@SpringBootApplication
public class AddressApplication{
	public static void main(String[] args){
		SpringApplication.run(AddressApplication.class, args);
	}
}

// SpringCacheManager 설정
@Configuration
public class RedisConfig{
	
	@Bean
	public RedisConnectionFactory connectionFactory(){
		return new LettuceConnectionFactory();
	}

	@Bean
	public RedisTemplate<Object, Object> redisTemplate() {
		RedisTemplate<Object, Object> redisTemplate = new RedisTemplate<>();
		redisTemplate.setConnectionFactory(connectionFactory());
		redisTemplate.setKeySerializer(new StringRedisSerializer());
		redisTemplate.setValueSerializer(new GenericJackson2JsonRedisSerializer());
		return redisTemplate;
	}

	@Bean
	public CacheManager redisCacheManager() {
		RedisCacheConfiguration redisCacheConfiguration = RedisCacheConfiguration
			.defaultCacheConfig()
			.serializeKeysWith(RedisSerializationContext
				.SerializationPair
				.fromSerializer(new StringRedisSerializer()))
			.serializeValuesWith(RedisSerializationContext
				.SerializationPair
				.fromSerializer(new GenericJackson2JsonRedisSerializer()))
			.entryTtl(Duration.ofMinutes(5L));

		RedisCacheManager cacheManager = RedisCacheManager
			.RedisCacheManagerBuilder
			.fromConnectionFactory(connectionFactory())
			.cacheDefaults(redisCacheConfiguration)
			.build();

		return cacheManager;
	}
}

// 캐시 등록 및 조회 service
public class addressService{
	@Cacheable(value = "address.region", key = "#region", cacheManager = "redisCacheManager")
	public List<Address> searchByRegion(String region) {
		return addressLogic.searchByRegion(region);
	}
	@Scheduled(fixedDelay = 300000L) // 5분마다 캐시 갱신
	@Cacheable(value = "address.total", key = "total")
	public List<Address> searchTotal(){
		return addressLogic.searchTotal();
	}
}
```

### 3. MSA환경에서 BFF패턴
MSA(MicroService Architecture) : 하나의 큰 어플리케이션을 여러개의 작은 어플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍쳐  
![image](https://github.com/NoRuTnT/practice/assets/114069644/959306f6-5061-4293-ab98-d1ef7c0fdbbc)    

MSA 구조를 활용하면 서버를 분산시켜 서비스를 안정적으로 구동하고 유지 보수를 용이하게 할 수 있다는 장점이 있다. 하지만 MSA 프로젝트에서는 프론트엔드와 통신의 효율성을 고려한 설계가 필요한데 그 중 대표적으로 API 를 통합적으로 관리해 줄 수 있는 BFF (Backend For Frontend)가 있다. 프론트엔드에서는 한번의 클릭만으로 MSA의 여러 MS 에 접근해야 하는 경우가 발생한다. 이 때마다 각 MS 에 호출을 발생시켜야 하며 호출 마다 인증 절차를 거친 후 Response를 받아와야 하는 비효율이 발생하게 된다. BFF 를 활용한다면 프론트엔드는 각 서비스에 직접 통신을 할 필요 없이 BFF에 통신을 위임하게 된다. 프론트엔드와 BFF 가 통신을 하고 BFF 는 프론트엔드로부터 받은 Request 를 분리해 각 서비스에 Request 를 보낸다. BFF 는 각 서비스로부터 받은 Response를 조합해 프론트엔드로 Response 하게 되면 통신은 완료된다. BFF의 효율성을 극대화 하기 위해서는 위에서 설명한 WebFlux 와 같은 Asynchronous Non-blocking을 지원하는 프레임워크를 사용하는 것이 좋다. MSA 프로젝트를 설계한다면 프론트엔드가 각 MS 와 직접 통신을 하면서 발생하는 중복 인증절차를 줄이고 API 호출을 위임해 비동기 방식으로 분산된 데이터를 수집할 수 있는 BFF 의 활용을 고려해 볼만 하다.  
![image](https://github.com/NoRuTnT/practice/assets/114069644/901112a8-2360-49c5-b6ab-184372b6fa1d)    

### 4. Spring Framework Reactive Stack
![image](https://github.com/NoRuTnT/practice/assets/114069644/5354d524-4f2d-43a2-b8ca-96de20d4fa0c)  
Asynchronous Non-blocking 1/0 모델의 대표적인 예는 Spring Framework Reactive Stack 이다. Reactive Stack 에서 Non-blocking I/O 를 수행하기 위해 WebFlux 프레임 워크를 사용한다. WebFlux구조는 사용자들의 Request를 Event Loop를 통해 처리하며 하나의 Thread로 하나의 작업을 처리하던 기 존의 Spring MVC 방식과 다르게 하나의 Thread 가 여러 작업을 처리 가능하다. WebFlux 의 성능을 최대로 활 용하기 위해서 작업을 처리하는 사이클 전반적 이벤트 처리는 Non-blocking 기반으로 구축되어야 한다. 예를 들어 WebFlux를 활용해 Non-blocking 방식으로 Request를 보내더라도 접근한 데이터베이스에서 Non-blo cking을 지원하지 않는다면 데이터베이스 접근 인터페이스에서 Blocking 이 발생하게 되므로 Reactive stack을 활용할 시 Mongo, Cassandra, Redis, Couchbase 등 Non-blocking을 지원하는 DBMS를 채택해야 한다.  
#### Blocking I/O와 Non-blocking I/O 의 코드 비교.
**Blocking I/O**  

```
@Test
public void blocking() {
    final RestTemplate restTemplate = new RestTemplate();

    for (int i = 0; i < 3; i++) {
				// spring 내장 클래스인 restTemplate 을 활용한 api 
        final ResponseEntity<String> response =
                restTemplate.exchange(THREE_SECOND_URL, HttpMethod.GET, HttpEntity.EMPTY, String.class);
        assertThat(response.getBody()).contains("success");
    }
}
// Blocking I/O 방식으로 api 호출 시 마다 blocking 발생
```

**Non-blocking I/O**  
```
@Test
public void nonBlocking() throws InterruptedException {
    for (int i = 0; i < LOOP_COUNT; i++) {
				// nonBlocking 방식인 webFlux 의 webClient 를 활용한 api	
        this.webClient
                .get()
                .uri(THREE_SECOND_URL)
                .retrieve()
                .bodyToMono(String.class)
                .subscribe(it -> {
                    count.countDown();
                    System.out.println(it);
                });
    }
    count.await(10, TimeUnit.SECONDS);
}

// LOOP_COUNT 를 증가시키더라도 결과 반환까지 시간이 크게 증가하지 않는다.
```

## 대규모 트래픽처리 면접에서 물어보면?
(scale-up, scale-out, 로드밸런싱, 캐싱을통한 DB부하개선)+ DB쿼리문개선, API코드개선 등 설명하면될듯?
