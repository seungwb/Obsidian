
| 어노테이션                      | 설명                                                                                                  |
| -------------------------- | --------------------------------------------------------------------------------------------------- |
| `@Getter`                  | 클래스의 모든 필드에 대한 getter 메서드를 자동 생성                                                                    |
| `@Setter`                  | 클래스의 모든 필드에 대한 setter 메서드를 자동 생성                                                                    |
| `@ToString`                | `toString()` 메서드를 자동 생성 (필드 정보를 출력)                                                                 |
| `@EqualsAndHashCode`       | `equals()` 및 `hashCode()` 메서드를 자동 생성                                                                |
| `@NoArgsConstructor`       | 기본 생성자(파라미터 없는 생성자) 자동 생성                                                                           |
| `@AllArgsConstructor`      | 모든 필드를 포함하는 생성자 자동 생성                                                                               |
| `@RequiredArgsConstructor` | `final` 혹은 `@NonNull` 필드만 포함한 생성자 자동 생성                                                             |
| `@Data`                    | `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, `@RequiredArgsConstructor` 포함              |
| `@Builder`                 | 빌더 패턴을 자동 생성                                                                                        |
| `@Value`                   | 불변 객체(Immutable Class) 생성 (`@Getter`, `@ToString`, `@AllArgsConstructor`, `private final 필드` 포함)    |
| `@Slf4j`                   | 로깅(Logger) 객체 자동 생성 (`private static final Logger log = LoggerFactory.getLogger(ClassName.class);`) |
