# redis에서 RDB와 AOF를 동시에 사용할 수 있는가?

---

결론은 yes이다.

이 둘을 활용하는 것은 redis.conf에서 aof-use-rdb-preamble yes로 설정할 수 있다.

5.0부터 기본값이 yes로 바뀌었다고 한다.

아래는 왜 둘을 동시에 사용하는 것이 좋은지에 대한 설명

RDB(Snapshot) VS AOF(Append only file)
 
RDB 방식은 저장하는데 AOF 방식보다 시간이 오래 걸립니다. 하지만 프로그램을 재시작할때 AOF에 비해 로딩 시간이 빠릅니다.

반면 AOF 방식은 모든 write/update 명령어를 모두 log 파일에 기록합니다. 즉 append만 하기 때문에 쓰는 시간이 RDB보다 빠릅니다. 하지만 프로그램을 재시작할때 모든 명령어를 읽어야 하기 때문에 로딩이 RDB보다 느립니다.

따라서 현재 Redis를 활용할 때는 이 둘을 적절히 혼용해서 사용합니다. 이 둘을 혼용하면 RDB가 만든 특정 스냅샷부터만 AOF 파일을 만들면 되기 때문에 둘의 장단점을 서로 보완할 수 있습니다.

이 둘을 활용하는 것은 redis.conf에서 aof-use-rdb-preamble yes로 설정할 수 있습니다. 5.0부터 기본값이 yes로 바뀌었습니다.

Reference

---

https://velog.io/@lhs8701/Redis-%EC%A0%95%EB%B3%B5%EA%B8%B0-1%ED%8E%B8-%EB%B0%B1%EC%97%85
 
https://inpa.tistory.com/entry/REDIS-%F0%9F%93%9A-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%98%81%EA%B5%AC-%EC%A0%80%EC%9E%A5%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98-%EC%98%81%EC%86%8D%EC%84%B1
 
https://stackoverflow.com/questions/63436459/redis-load-from-rdb-and-keep-writing-the-aof
 
https://github.com/redis/redis/blob/6.0.6/redis.conf#L1157
 
http://redisgate.kr/redis/configuration/param_aof-use-rdb-preamble.php
