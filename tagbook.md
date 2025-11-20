# Tagbook - Loja Fictícia E-commerce

---

## 1 Eventos Implementados

### 1.1 Evento: `view_item_list`

**Quando dispara:** No carregamento da página `index.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'view_item_list',
  ecommerce: {
    item_list_id: 'homepage_products',
    item_list_name: 'Home - Lista de Produtos',
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90,
        item_list_name: 'Home - Lista de Produtos',
        item_list_id: 'homepage_products',
        index: 1
      },
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "view_item_list" |
| `ecommerce.item_list_id` | string | ID da lista | "homepage_products" |
| `ecommerce.item_list_name` | string | Nome da lista | "Home - Lista de Produtos" |
| `ecommerce.items` | array | Array de produtos | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |
| `ecommerce.items[].index` | number | Posição na lista | 1 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - view_item_list"
- **Tag:** GA4 - Evento - view_item_list
  - Nome do evento: `view_item_list`
  - Parâmetros do evento:
    - `item_list_id` = `{{ecommerce.item_list_id}}`
    - `item_list_name` = `{{ecommerce.item_list_name}}`
    - `items` = `{{ecommerce.items}}`

---

### 1.2 Evento: `view_item`

**Quando dispara:** No carregamento da página `product.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'view_item',
  ecommerce: {
    currency: 'BRL',
    value: 79.90,
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90
      }
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "view_item" |
| `ecommerce.currency` | string | Código da moeda | "BRL" |
| `ecommerce.value` | number | Valor total | 79.90 |
| `ecommerce.items` | array | Array com o produto | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - view_item"
- **Tag:** GA4 - Evento - view_item
  - Nome do evento: `view_item`
  - Parâmetros do evento:
    - `currency` = `{{ecommerce.currency}}`
    - `value` = `{{ecommerce.value}}`
    - `items` = `{{ecommerce.items}}`

---

### 1.3 Evento: `add_to_cart`

**Quando dispara:** Ao clicar no botão `#add-to-cart-btn` em `product.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'add_to_cart',
  ecommerce: {
    currency: 'BRL',
    value: 79.90, // price * quantity
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90,
        quantity: 1
      }
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "add_to_cart" |
| `ecommerce.currency` | string | Código da moeda | "BRL" |
| `ecommerce.value` | number | Valor total (preço × qtd) | 79.90 |
| `ecommerce.items` | array | Array com o produto | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |
| `ecommerce.items[].quantity` | number | Quantidade adicionada | 1 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - add_to_cart"
- **Tag:** GA4 - Evento - add_to_cart
  - Nome do evento: `add_to_cart`
  - Parâmetros do evento:
    - `currency` = `{{ecommerce.currency}}`
    - `value` = `{{ecommerce.value}}`
    - `items` = `{{ecommerce.items}}`

**Observações:**
- O link do botão "Adicionar ao carrinho" foi alterado para `href="#"` para controlar a ação com JavaScript. 
- O script do evento `add_to_cart` está localizado no final do `<body>` (antes de `</footer>`) para garantir que o botão já exista no DOM quando o event listener for adicionado.
- Inclui um `setTimeout` de 300ms para garantir que o GTM processe o evento antes do redirecionamento para o carrinho.

---

### 1.4 Evento: `view_cart`

**Quando dispara:** No carregamento da página `cart.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'view_cart',
  ecommerce: {
    currency: 'BRL',
    value: 79.90,
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90,
        quantity: 1
      }
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "view_cart" |
| `ecommerce.currency` | string | Código da moeda | "BRL" |
| `ecommerce.value` | number | Valor total do carrinho | 79.90 |
| `ecommerce.items` | array | Produtos no carrinho | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |
| `ecommerce.items[].quantity` | number | Quantidade | 1 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - custom - view_cart"
- **Tag:** GA4 - Evento - view_cart
  - Nome do evento: `view_cart`
  - Parâmetros do evento:
    - `currency` = `{{ecommerce.currency}}`
    - `value` = `{{ecommerce.value}}`
    - `items` = `{{ecommerce.items}}`

---

### 1.5 Evento: `begin_checkout`

**Quando dispara:** No carregamento da página `checkout.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'begin_checkout',
  ecommerce: {
    currency: 'BRL',
    value: 79.90,
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90,
        quantity: 1
      }
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "begin_checkout" |
| `ecommerce.currency` | string | Código da moeda | "BRL" |
| `ecommerce.value` | number | Valor total | 79.90 |
| `ecommerce.items` | array | Produtos sendo comprados | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |
| `ecommerce.items[].quantity` | number | Quantidade | 1 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - begin_checkout"
- **Tag:** GA4 - Evento - begin_checkout
  - Nome do evento: `begin_checkout`
  - Parâmetros do evento:
    - `currency` = `{{ecommerce.currency}}`
    - `value` = `{{ecommerce.value}}`
    - `items` = `{{ecommerce.items}}`

---

### 1.6 Evento: `purchase`

**Quando dispara:** No carregamento da página `thankyou.html`

**Exemplo de payload JSON:**
```javascript
{
  event: 'purchase',
  ecommerce: {
    transaction_id: 'PEDIDO12345',
    value: 79.90,
    tax: 0.00,
    shipping: 10.00,
    currency: 'BRL',
    coupon: '',
    items: [
      {
        item_id: 'SKU123',
        item_name: 'Camiseta Básica Branca',
        item_category: 'Vestuário',
        price: 79.90,
        quantity: 1
      }
    ]
  }
}
```

**Campos enviados:**
| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| `event` | string | Nome do evento | "purchase" |
| `ecommerce.transaction_id` | string | ID único da transação | "PEDIDO12345" |
| `ecommerce.value` | number | Valor dos produtos | 79.90 |
| `ecommerce.tax` | number | Valor dos impostos | 0.00 |
| `ecommerce.shipping` | number | Valor do frete | 10.00 |
| `ecommerce.currency` | string | Código da moeda | "BRL" |
| `ecommerce.coupon` | string | Cupom utilizado | "" |
| `ecommerce.items` | array | Produtos comprados | [...] |
| `ecommerce.items[].item_id` | string | SKU do produto | "SKU123" |
| `ecommerce.items[].item_name` | string | Nome do produto | "Camiseta Básica Branca" |
| `ecommerce.items[].item_category` | string | Categoria | "Vestuário" |
| `ecommerce.items[].price` | number | Preço unitário | 79.90 |
| `ecommerce.items[].quantity` | number | Quantidade comprada | 1 |

**Configuração no GTM:**
- **Acionador:** Evento personalizado = "custom - purchase"
- **Tag:** GA4 - Evento - purchase
  - Nome do evento: `purchase`
  - Parâmetros do evento:
    - `transaction_id` = `{{ecommerce.transaction_id}}`
    - `value` = `{{ecommerce.value}}`
    - `tax` = `{{ecommerce.tax}}`
    - `shipping` = `{{ecommerce.shipping}}`
    - `currency` = `{{ecommerce.currency}}`
    - `coupon` = `{{ecommerce.coupon}}`
    - `items` = `{{ecommerce.items}}`

---

## 2 Configuração do Google Tag Manager

### 2.1 Tags Criadas

| Nome da Tag | Tipo | Evento GA4 | Acionador |
|-------------|------|------------|---------|
| Tag Google | Tag do Google | - | Initialization - All Pages |
| GA4 - Evento - view_item_list | Evento do GA4 | view_item_list | custom - view_item_list |
| GA4 - Evento - view_item | Evento do GA4 | view_item | custom - view_item |
| GA4 - Evento - add_to_cart | Evento do GA4 | add_to_cart | custom - add_to_cart |
| GA4 - Evento - view_cart | Evento do GA4 | view_cart | custom - view_cart |
| GA4 - Evento - begin_checkout | Evento do GA4 | begin_checkout | custom - begin_checkout |
| GA4 - Evento - purchase | Evento do GA4 | purchase | custom - purchase |

### 2.2 Acionadors Criados

| Nome do Acionador | Tipo | Condição |
|-----------------|------|----------|
| Initialization - All Pages | Page View | All Pages |
| custom - view_item_list | Evento personalizado | Event equals "view_item_list" |
| custom - view_item | Evento personalizado | Event equals "view_item" |
| custom - add_to_cart | Evento personalizado | Event equals "add_to_cart" |
| custom - view_cart | Evento personalizado | Event equals "view_cart" |
| custom - begin_checkout | Evento personalizado | Event equals "begin_checkout" |
| custom - purchase | Evento personalizado | Event equals "purchase" |

### 2.3 Variáveis Criadas

| Nome da Variável | Tipo | Nome da Variável da Camada de Dados  |
|------------------|------|--------------------------|
| ecommerce.coupon | Variável da camada de dados | ecommerce.coupon |
| ecommerce.currency | Variável da camada de dados | ecommerce.currency |
| ecommerce.item_list_id | Variável da camada de dados | ecommerce.item_list_id |
| ecommerce.item_list_name | Variável da camada de dados | ecommerce.item_list_name |
| ecommerce.items | Variável da camada de dados | ecommerce.items |
| ecommerce.shipping | Variável da camada de dados | ecommerce.shipping |
| ecommerce.tax | Variável da camada de dados | ecommerce.tax |
| ecommerce.transaction_id | Variável da camada de dados | ecommerce.transaction_id |
| ecommerce.value | Variável da camada de dados | ecommerce.value |

---

## 3 Método de Extração de Dados

Os dados dos produtos são extraídos diretamente dos atributos `data-*` presentes nos elementos HTML:
```html
<article class="product-card"
  data-product-id="SKU123"
  data-product-name="Camiseta Básica Branca"
  data-product-category="Vestuário"
  data-product-price="79.90">
```

JavaScript lê esses atributos usando:
```javascript
const productId = element.dataset.productId;
const productName = element.dataset.productName;
// etc...
```

---

## 4 Testes Realizados

### 4.1 Modo de Visualização do GTM
Todos os eventos foram testados usando o modo de visualização (Preview Mode) do Google Tag Manager conectado ao servidor local.

### 4.2 Resultados dos Testes

| Evento | Status | Data Layer Populado | Tag Disparada |
|--------|--------|---------------------|---------------|
| view_item_list | ✅ Aprovado | Sim | Sim |
| view_item | ✅ Aprovado | Sim | Sim |
| add_to_cart | ✅ Aprovado | Sim | Sim |
| view_cart | ✅ Aprovado | Sim | Sim |
| begin_checkout | ✅ Aprovado | Sim | Sim |
| purchase | ✅ Aprovado | Sim | Sim |

---

Criado por Victor Machado
