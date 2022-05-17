---
title:  "스프링 REST 튜토리얼 따라해보기 4: 링크 생성 단순화하기"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - spring

date: 2022-05-12
last_modified_at: 2022-05-12
sitemap:
  changefreq: daily
  priority: 1.0
---

# 개요

이전 포스트에서 조금 더 RESTful 한 서비스를 제공하기 위해 링크를 추가해보았습니다.

이번 포스트에서는 중복되는 코드를 줄이기 위해 RepresentationModelAssembler 를 사용해보겠습니다.



# RepresentationModelAssembler

Spring HATEOAS 에서 제공하는 인터페이스입니다. 이전 포스트에서 단일 조회 메서드와 전체 조회 메서드에서 다음 코드가 반복되었었습니다.

```java
linkTo(methodOn(EmployeeController.class).one(employee.getId())).withSelfRel(),
          linkTo(methodOn(EmployeeController.class).all()).withRel("employees")))
```

중복을 줄이기 위해 RepresentationModelAssembler 인터페이스를 활용해보겠습니다.



RepresentationModelAssembler 를 구현하는 EmployeeModelAssembler 를 다음과 같이 생성합니다.

```java
package payroll;

import static org.springframework.hateoas.server.mvc.WebMvcLinkBuilder.*;

import org.springframework.hateoas.EntityModel;
import org.springframework.hateoas.server.RepresentationModelAssembler;
import org.springframework.stereotype.Component;

@Component
class EmployeeModelAssembler implements RepresentationModelAssembler<Employee, EntityModel<Employee>> {

  @Override
  public EntityModel<Employee> toModel(Employee employee) {

    return EntityModel.of(employee, //
        linkTo(methodOn(EmployeeController.class).one(employee.getId())).withSelfRel(),
        linkTo(methodOn(EmployeeController.class).all()).withRel("employees"));
  }
}
```



# DI

위에서 만든 EmployeeModelAssembler 구현체를 EmployeeController 에 의존성 주입해주겠습니다.

우리는 Lombok 의 @RequiredArgsConstructor 에너테이션을 사용하고 있으므로 다음 코드 한 줄을 추가해주면 됩니다.

```java
private final EmployeeModelAssembler assembler;
```



# 단일 조회 메서드 수정

새롭게 만든 assembler 를 이용하여 다음과 같이 one 메서드를 수정합니다.

```java
@GetMapping("/employees/{id}")
EntityModel<Employee> one(@PathVariable Long id) {

  Employee employee = repository.findById(id) //
      .orElseThrow(() -> new EmployeeNotFoundException(id));

  return assembler.toModel(employee);
}
```



# 전체 조회 메서드 수정

all 메서드도 다음과 같이 변경합니다.

```java
@GetMapping("/employees")
CollectionModel<EntityModel<Employee>> all() {

  List<EntityModel<Employee>> employees = repository.findAll().stream() //
      .map(assembler::toModel) //
      .collect(Collectors.toList());

  return CollectionModel.of(employees, linkTo(methodOn(EmployeeController.class).all()).withSelfRel());
}
```



# 출처

* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)