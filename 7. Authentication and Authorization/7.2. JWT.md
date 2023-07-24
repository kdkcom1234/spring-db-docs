```groovy

implementation 'com.auth0:java-jwt:3.18.2'

```

당신이 요청한대로, `sub`, `name`, `iat`, `role`이라는 필드가 포함된 페이로드로 JWT를 생성하고, 이를 검증하고 해당 페이로드를 추출하는 Java 예제를 아래에 제시하겠습니다. 이 예제에서는 `java-jwt` 라이브러리를 사용합니다.

```java
import com.auth0.jwt.JWT;
import com.auth0.jwt.JWTCreator;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.exceptions.JWTVerificationException;
import com.auth0.jwt.interfaces.Claim;
import com.auth0.jwt.interfaces.DecodedJWT;
import com.auth0.jwt.interfaces.JWTVerifier;

import java.util.Date;
import java.util.Map;

public class JWTExample {

    private static final String SECRET = "your-secret-key"; // 이 비밀 키는 저장하거나 공유하지 않도록 주의하세요.

    public static void main(String[] args) {
        // JWT 토큰 생성
        String token = createToken();

        System.out.println("Generated JWT: " + token);

        // JWT 토큰 검증 및 페이로드 추출
        try {
            Map<String, Claim> claims = verifyToken(token);
            // 페이로드 값 추출
            Claim sub = claims.get("sub");
            Claim name = claims.get("name");
            Claim iat = claims.get("iat");
            Claim role = claims.get("role");

            System.out.println("sub: " + sub.asString());
            System.out.println("name: " + name.asString());
            System.out.println("iat: " + iat.asDate());
            System.out.println("role: " + role.asString());
        } catch (JWTVerificationException exception) {
            // JWT 토큰이 유효하지 않음
            System.out.println("Invalid token");
        }
    }

    private static String createToken() {
        Algorithm algorithm = Algorithm.HMAC256(SECRET);
        JWTCreator.Builder builder = JWT.create()
                .withIssuer("your-app") // 발행자 설정
                .withIssuedAt(new Date()) // 토큰 발행 시간 설정
                .withExpiresAt(new Date(System.currentTimeMillis() + 3600 * 1000)) // 만료 시간 설정 (1시간 뒤 만료)
                .withSubject("1234567890") // 'sub' 설정
                .withClaim("name", "John Doe") // 'name' 설정
                .withClaim("role", "admin"); // 'role' 설정

        return builder.sign(algorithm);
    }

    private static Map<String, Claim> verifyToken(String token) throws JWTVerificationException {
        Algorithm algorithm = Algorithm.HMAC256(SECRET);
        JWTVerifier verifier = JWT.require(algorithm)
                .withIssuer("your-app") // 발행자 확인
                .build();

        DecodedJWT jwt = verifier.verify(token);
        return jwt.getClaims();
    }
}
```

위 코드에서 `sub`, `name`, `iat`, `role` 필드를 페이로드에 추가하였으며, 이를 검증하는 부분에서 해당 필드를 추출하였습니다. 또한, 비밀 키 `SECRET`는 절대로 외부에 노출되어서는 안되며 안전하게 보관되어야 한다는 점을 잊지 마세요.
