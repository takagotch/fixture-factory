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

Fixture.from(Client.class).uses(new HibernateProcessor(session)).gimme("valid");

Fixture.of(Order.class).addTemplate("valid", new Rule() {{
  add("id", random(Long.class, range(1L, 200L)));
  add("items", has(3).of(Item.class, "valid", "invalid", "external"));
  add("payment", one(Payment.class, "valid"));
}});

Fixture.of(Item.class).addTemplate("valid", new Rule() {{
  add("productId", random(Integer.class, range(1L, 200L)));
}});

Fixture.of(Payment.class).addTemplate("valid", new Rule() {{
  add("id", random(Long.class, range(1L, 200L)));
}});

Fixture.of(Any.class).addTEmplate("valid", new Rule() {{
  add("id", regex("\\d{3,5}"));
  add("phoneNumber", regex("(\\d{2}-(\\d{4}-(\\d{4})"))));
}});

Fixture.of(Any.class).addTemplate("valid", new Rule() {{
  add("dueDate", beforeDate("2011-04-15", new SimpleDateFormat("yyyy-MM-dd")));
  add("payDate", afterDate("2011-04-15", new SimpleDateFormat("yyyy-MM-dd")));
  add("birthday", randomDate("2011-04-15", "2011-11-07", new SimpleDateFormat("yyyy-MM-dd")));
  add("cutDate", instant("now"));
}});

Fixture.of(Any.class).addTemplate("valid", new Rule() {{
  add("firstName", firstName());
  add("lastName", lastName());
}});

Fixture.of(Any.class).addTemplate("valid", new Rule() {{
  add("country", "Brazil");
  add("stete", uniqueRandom("Sao Paulo", "Rio de Janeiro", "Minas Gerais", "Bahia"));
}});

Fixture.of(User.class).addTemplate("valid", ne Rule() {{
  add("cnpj", cnpj());
  add("cnpj", cnpj(true));
}});
```

```
```

```
```


