### fixture-factory
---
https://github.com/six2six/fixture-factory

```java
Fixture.of(Client.class).addTemplate("valid", new Rule(){{

}});

Fixture.of(Address.class).addTemplate("valid", new Rule(){{
  add("id", random(Long.class, range(1L, 100L)));
  add("street", random("Paulista Avenue", "Ibirapuera Avenue"));
  add("city", "Sao Paulo");
  add("state", "${city}");
  add("country", "Brazil");
  add("zipCode", random("06608000", "17720000"));
}});

Fixture.of(Address.class).addTemplate("augustaStreet").inherits("valid", new Rule() {{
  add("street", "Augusta Street");
}});

Client client = Fixture.from(Client.class).gimme("valid");
List<Client> clients = Fixture.from(Client.class).gimme(5, "valid");

public class ClientTemplateLoader implements TemplateLoader {
  @Override
  public void load() {
    Fixture.of(Client.class).addTEmplate("valid", new Rule(){{
      add("id", random(Long.class, range(1L, 200L)));
      add("name", random("Anderson Parra", "Arthur Hirata"));
      add("nickname", random("nerd", "geek"));
      add("email", "${nickname}@gmail.com");
      add("birthday", instant("18 years ago"));
      add("address", one(Address.class, "valid"));
    }});
    
    Fixture.of(Address.class).addTemplate("valid", new Rule() {{
      add("id", random(Long.class, range(1L, 100L)));
      add("street", random("Paulista Avenue", "Ibirapuera Avenue"));
      add("state", "#{city}");
      add("country", "Brazil");
      add("zipCode", random("06608000", "17720000"));
    }});
  }
}

FixtureFactoryLoader.loadTemplates("br.com.siz2six.template");

@BeforeClass
public static void setUp() {
  FixtureFactoryLoader.loadTemplates("br.com.siz2six.template");
}

public class MyCustomProcessor implements Processor {
  public void execute(Object object) {
    //
  }
}

Fixture.from(SomeClass.class).uses(new MyCustomProcessor()).gimme("someTemplate");


```

```
```

```
```


