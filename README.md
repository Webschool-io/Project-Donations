# Project-Donations

Sistema de gerenciamento de doações

Iniciamos a modelagem pelo Doador pois ele é o ator principal.

Doador:
- nome
- email
- cpf
- endereço
- telefone
- histórico de doações

Doação:
- valor
- doador
- projeto

Projeto:
- nome
- email
- cpf ou cnpj
- endereço
- telefone
- equipe
- custo mês
- orçamento

Orçamento:
- contas a pagar
  + aluguel
  + água
  + luz
  + internet
- equipe
- infra


## Metodologia

1. Definição das entidades
2. Definição dos Átomos
  2.1. Definição dos seus Quarks
3. Definição das Moléculas
4. Definição dos Organimos
5. Definição das Rotas

### Definição das entidades

Inicialmente definimos as entidades que fazem parte do sistema sem necessariamente modelar o banco.

Nesse passo não é definido qualquer tipo de ligação entre elas.

Entidades:

- Doador
- Doação
- Projeto
- Orçamento
- Fornecedor

### Definição dos Átomos

Nessa etapa definimos **todos** os Átomos(campos) necessários para o sistema, porém ainda sem ligarmos o Átomo à entidade, pois um mesmo átomo pode estar em mais de 1 Molécula.

Átomos:

- name
- email
- password
- telefones
  - tipo
  - ddd
  - numero
- endereço: 
  - logradouro
  - nome
  - numero
  - complemento
  - cep
  - estado
  - pais
- cpf
- cnpj
- razao_social
- responsavel_legal
- valor
- user_id
- doador_id
- doacao_id
- projeto_id
- fornecedor_id


#### Definição dos seus Quarks

Antes de definirmos quais Quarks fazem parte do Átomo precisamos criar todos eles.

Vamos começar pelos básicos:

- isEmpty
- isNumber
- isString
- isBoolean
- isDate

Depois deles podemos criar os Quarks específicos para campos:

- isUserID
- isName
- isEmail
- isPhone
  + isPhoneDDD
  + isPhoneNumber
- isCPF
- isCPNJ
- isRazaoSocial
- isAddress
  + isAddressType //logradouro
  + isAddressName
  + isAddressNumber
  + isAddressCEP
  + isAddressCity
  + isAddressState
  + isAddressCountry

Após a criação de todos os Quarks podemos partir para os Átomos em si.

Vamos seguir o seguinte padrão para **TODOS** os Átomos do Mongoose:

```js
const Atom = {
  type: String
, get: require()
, set: require()
, validate: require()
}

module.exports = Atom;
```

Agora com um exemplo que aprendemos em aula:

```js
const Atom = {
  type: String
, get: require('./../quarks/toUpper')
, set: require('./../quarks/toLower')
, validate: require('./../quarks/isEmptyStringValidate')
, required: true
, index: true
}

module.exports = Atom;
```

### Definição das Moléculas

Após a definição de **TODOS** os Átomos podemos iniciar as Moléculas.

A estrutura de uma Molécula do Mongoose é a seguinte:

```js
const Molecule = {
  nameAtom1: require('./../atoms/nameAtom1')
, nameAtom2: require('./../atoms/nameAtom2')
, ...
}
```

Ou seja, é um objeto que possui como atributo o nome do campo(Átomo) e como valor o módulo desse Átomo, ficando assim:

```js
'use strict';

const mongoose = require('mongoose');

const Molecule = {
  name: require('./../atoms/atom-name')
, email: require('./../atoms/atom-email')
, password: require('./../atoms/atom-password')
, phones: [
    { type: require('./../atoms/atom-phone-type')
    , ddd: require('./../atoms/atom-phone-ddd')
    , number: require('./../atoms/atom-phone-number')
    }
  ]
}
module.exports = new mongoose.Schema(Molecule);
```

### Definição dos Organimos

### Definição das Rotas

## Reuniões

### 04/03/2016 - Primeira

Possíveis features:

- Escolha de fornecedores por licitação ou automático com parceiros
- Impressão para abate no IR
- Pedido de cpf/cnpj



