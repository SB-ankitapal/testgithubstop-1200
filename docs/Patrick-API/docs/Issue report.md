---
stoplight-id: huzy7yqo0tamu
---

---

## stoplight-id: bdb05939e31aa

# Issue 1 - Export is adding "extension" from another model

## Problematic description

Why Animal.1 is getting "x-proto-indexes" after the export ?

see file : .. /exports/Export_animal.v.1.0.yaml

```json
  Animal.v1:
    x-proto-indexes: 100
```

## Source:

see file : ../models/Animal.v1.yaml

see file : ../models/Bird.v1.yaml

File : Animal.v1.yaml
```json
title: Animal.v1
x-stoplight:
  id: qp28gx88c56yu
type: object
properties:
  id:
    type: string
  legs:
    type: string
description: Abstract Animal
```
File : Animal.v1.yaml
```json
x-stoplight:
  id: hia6y2qoyaa0m
description: Bird description
type: object
properties:
  animal:
    $ref: ./Animal.v1.yaml
    description: bird animal
    x-proto-indexes: 100
  isflying:
    type: string
    x-proto-indexes: 2
```

## Export result:

```json
definitions:
  Animal.v1:
    description: bird animal 
    x-proto-indexes: 100      <---- Why
    title: Animal.v1
    x-stoplight:
      id: qp28gx88c56yu
    type: object
    properties:
      id:
        type: string
      legs:
        type: string
  Bird.v1:
    x-stoplight:
      id: hia6y2qoyaa0m
    description: Bird description
    type: object
    properties:
      animal:
        $ref: '#/definitions/Animal.v1'
        description: bird animal
        x-proto-indexes: 100
      isflying:
        type: string
        x-proto-indexes: 2
```

# Issue 2 - Export is overriding description (and should not)

## Problematic description

Why Animal.1 is not keepig its description " after the export ?

see file : .. /exports/Export_animal.v.1.0.yaml

```json
  Animal.v1:
    description: bird animal
```

it should be "Abstract Animal"


## Source:

see file : ../models/Animal.v1.yaml

see file : ../models/Bird.v1.yaml

File : Animal.v1.yaml
```json
title: Animal.v1
x-stoplight:
  id: qp28gx88c56yu
type: object
properties:
  id:
    type: string
  legs:
    type: string
description: Abstract Animal
```
File : Animal.v1.yaml
```json
x-stoplight:
  id: hia6y2qoyaa0m
description: Bird description
type: object
properties:
  animal:
    $ref: ./Animal.v1.yaml
    description: bird animal
    x-proto-indexes: 100
  isflying:
    type: string
    x-proto-indexes: 2
```

## Export result:

```json
definitions:
  Animal.v1:
    description: bird animal  <---- Why
    x-proto-indexes: 100      
    title: Animal.v1
    x-stoplight:
      id: qp28gx88c56yu
    type: object
    properties:
      id:
        type: string
      legs:
        type: string
  Bird.v1:
    x-stoplight:
      id: hia6y2qoyaa0m
    description: Bird description
    type: object
    properties:
      animal:
        $ref: '#/definitions/Animal.v1'
        description: bird animal
        x-proto-indexes: 100
      isflying:
        type: string
        x-proto-indexes: 2
```

## EXPECTED result:

```json
definitions:
  Animal.v1:
    description: Abstract Animal  <---- Here     
    title: Animal.v1
    type: object
    properties:
      id:
        type: string
      legs:
        type: string
  Bird.v1:
    description: Bird description
    title: Bird.v1
    type: object
    properties:
      animal:
        $ref: '#/definitions/Animal.v1'
        description: bird animal
        x-proto-indexes: 100
      isflying:
        type: string
        x-proto-indexes: 2
```



# Missing feature: Extension at field level

## Problematic description

![image.png](../assets/images/image.png)

## Expectation

```json
x-stoplight:
  id: hia6y2qoyaa0m
description: Bird description
type: object
properties:
  animal:
    $ref: ./Animal.v1.yaml
    description: bird animal
    x-proto-indexes: 100   <--  Here
  isflying:
    type: string
    x-proto-indexes: 2   <--  Here
```


# Missing feature  : Impossible to export (md) as PDF

# Issue with TOC:

Not following Headings

![image.png](../assets/images/image-2.png)

