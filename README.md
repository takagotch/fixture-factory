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




```

```
```

```
```


