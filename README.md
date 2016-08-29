# Spock

Groovy を使用して、Spec ベースのテストを記述できるようにしたフレームワークが Spock です。
`where` というキーワードを使用して、あらゆるテスティングフレームワークよりも圧倒的に効率良く、パターンテストを記述できるようにしているのが特徴です。
また、導入についても依存関係を追加するだけなので非常に簡単に始められるのも特徴です。

各テスティング手法との用語マッピング

| TDD            | BDD   | TDD/BDD     |
| JUnit          | Spec  | Spock       |
|:--------------:|:-----:|:-----------:|
| Before/Setup   | Given | Setup/Given |
| Test           |       | Expect      |
| Rule           |       | Where       |
|                | On    | When        |
|                | It    | Then        |
| After/TearDown |       | Cleanup     |

## How to use

依存関係に、Groovy と、Spock を追加したら、使用準備はそれだけで完了です。
(Spring DI を組み合わせる場合には、更に依存が必要。)

```
<dependency>
    <groupId>org.codehaus.groovy</groupId>
    <artifactId>groovy-all</artifactId>
    <version>2.4.7</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.spockframework</groupId>
    <artifactId>spock-core</artifactId>
    <version>1.0-groovy-2.4</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.spockframework</groupId>
    <artifactId>spock-spring</artifactId>
    <version>1.0-groovy-2.4</version>
    <scope>test</scope>
</dependency>
```

テストコードの簡単なサンプルは、以下のようになります。

```
class HogeSpec extends Specification {
    @Shared
    def hoge;

    def setup() {
        hoge = new Hoge();
    }
    
    def "print( #prmNumber ) で 'hoge' が #prmNumber 回表示される"() {
        expect:
        assert #expPrint == hoge.print( prmNumber )
        
        where:
        prmNumber | expPrint
        1         | 'hoge'
        2         | 'hogehoge'
    }
}
```


# DbSetup

```
<dependency>
    <groupId>com.googlecode.log4jdbc</groupId>
    <artifactId>log4jdbc</artifactId>
    <version>1.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>com.ninja-squad</groupId>
    <artifactId>DbSetup</artifactId>
    <version>2.1.0</version>
    <scope>test</scope>
</dependency>
```