
# 🅰️ Guia Completo de Angular

Este guia cobre os principais conceitos, práticas e comandos do Angular, do básico ao avançado.

---

## 📚 Sumário

1. [O que é Angular?](#1-o-que-é-angular)
2. [Instalação do Angular CLI](#2-instalação-do-angular-cli)
3. [Criando um novo projeto](#3-criando-um-novo-projeto)
4. [Estrutura de pastas do Angular](#4-estrutura-de-pastas-do-angular)
5. [Componentes](#5-componentes)
6. [Serviços e Injeção de Dependência](#6-serviços-e-injeção-de-dependência)
7. [Data Binding](#7-data-binding)
8. [Diretivas](#8-diretivas)
9. [Pipes](#9-pipes)
10. [Roteamento (Routing)](#10-roteamento-routing)
11. [Formulários](#11-formulários)
12. [Requisições HTTP](#12-requisições-http)
13. [Ciclo de Vida dos Componentes](#13-ciclo-de-vida-dos-componentes)
14. [Módulos](#14-módulos)
15. [Guards e Rotas Protegidas](#15-guards-e-rotas-protegidas)
16. [Testes em Angular](#16-testes-em-angular)
17. [Build para Produção](#17-build-para-produção)
18. [Boas Práticas](#18-boas-práticas)

---

## 1. O que é Angular?

Angular é um framework de front-end baseado em TypeScript mantido pelo Google. Ele permite criar aplicações web de página única (SPA) de forma escalável, performática e modular.

---

## 2. Instalação do Angular CLI

```bash
npm install -g @angular/cli
```

Verificar a versão:

```bash
ng version
```

---

## 3. Criando um novo projeto

```bash
ng new nome-do-projeto
cd nome-do-projeto
ng serve
```

Acesse [http://localhost:4200](http://localhost:4200)

---

## 4. Estrutura de pastas do Angular

- `src/app`: Onde fica o código principal da aplicação
- `app.component.*`: Primeiro componente renderizado
- `assets`: Arquivos estáticos
- `environments`: Configurações de ambiente (dev/prod)

---

## 5. Componentes

Criados com:

```bash
ng generate component nome
# ou
ng g c nome
```

Um componente contém:
- `.ts`: Lógica
- `.html`: Template
- `.css`: Estilo
- `.spec.ts`: Teste

---

## 6. Serviços e Injeção de Dependência

Criar um serviço:

```bash
ng generate service nome
```

Usado para lógica reutilizável (HTTP, armazenamento, etc.).

Injeção via construtor:

```ts
constructor(private meuServico: MeuServico) {}
```

---

## 7. Data Binding

Tipos:
- **Interpolation**: `{{ nome }}`
- **Property binding**: `[src]="url"`
- **Event binding**: `(click)="acao()"`
- **Two-way binding**: `[(ngModel)]="valor"`

---

## 8. Diretivas

### Estruturais
- `*ngIf`: Condicional
- `*ngFor`: Repetição
- `*ngSwitch`

### Atributo
- `[ngClass]`, `[ngStyle]`

---

## 9. Pipes

## 📌 O que são Pipes?
- Pipes são operadores usados em templates Angular para transformar dados de forma declarativa.
- Utilizam o caractere `|` (pipe) e funcionam como funções de transformação.
- Exemplo: `{{ amount | currency }}`

---

## 🧰 Pipes Embutidos (Built-in)
| Nome              | Descrição                                                                 |
|-------------------|---------------------------------------------------------------------------|
| `AsyncPipe`       | Lê valores de `Promise` ou `Observable`.                                 |
| `CurrencyPipe`    | Formata número como moeda conforme a localidade.                         |
| `DatePipe`        | Formata datas conforme a localidade.                                     |
| `DecimalPipe`     | Formata números decimais.                                                 |
| `I18nPluralPipe`  | Pluralização com base em regras locais.                                  |
| `I18nSelectPipe`  | Seleção de valores com base em chaves.                                   |
| `JsonPipe`        | Transforma objeto em string JSON (útil para debug).                      |
| `KeyValuePipe`    | Transforma objetos/Map em arrays de chave-valor.                         |
| `LowerCasePipe`   | Texto para letras minúsculas.                                             |
| `UpperCasePipe`   | Texto para letras maiúsculas.                                             |
| `PercentPipe`     | Formata número como percentual.                                           |
| `SlicePipe`       | Retorna uma parte de um array ou string.                                 |
| `TitleCasePipe`   | Texto para título (primeira letra maiúscula de cada palavra).            |

---

## 🧪 Como usar Pipes
```html
<!-- Aplica o pipe de moeda -->
<p>Total: {{ amount | currency }}</p>
```

## 🔗 Combinando múltiplos pipes
```html
<!-- Primeiro aplica date e depois uppercase -->
<p>{{ scheduledOn | date | uppercase }}</p>
```

## ⚙️ Passando parâmetros para Pipes
```html
<!-- Formata a hora -->
<p>{{ scheduledOn | date:'hh:mm' }}</p>

<!-- Formata a hora e define fuso horário -->
<p>{{ scheduledOn | date:'hh:mm':'UTC' }}</p>
```

---

## 🧠 Como Pipes funcionam
- Pipes são **funções puras** por padrão: só executam quando o valor de entrada muda.
- Isso evita cálculos desnecessários e melhora a performance.

## 🔢 Precedência de operadores
- Pipe (`|`) tem **baixa precedência**, por isso use parênteses:
```html
{{ (firstName + lastName) | uppercase }}
```

---

## 🛠️ Criando Pipes personalizados

### 1. Estrutura básica
```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'kebabCase' })
export class KebabCasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toLowerCase().replace(/ /g, '-');
  }
}
```

### 2. Nomeação
- Nome do pipe: **camelCase**
- Nome da classe: **PascalCase + Pipe**

### 3. Adicionando parâmetros
```ts
transform(value: string, format: string): string {
  return format === 'uppercase' ? value.toUpperCase() : value;
}
```

---

## ⚠️ Pipes Impuros
- Detectam mudanças **internas** em objetos/arrays.
- São marcados com `pure: false` (evite se possível por motivos de performance).

```ts
@Pipe({ name: 'joinNamesImpure', pure: false })
export class JoinNamesImpurePipe implements PipeTransform {
  transform(names: string[]): string {
    return names.join();
  }
}
```

---

## 📚 Conclusão
- Pipes são poderosos para formatar e transformar dados em templates.
- Prefira pipes puros sempre que possível.
- Use pipes personalizados para reutilizar lógicas de transformação.

## 10. Roteamento (Routing)

Definido em `app-routing.module.ts`.

Exemplo:

```ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'produtos', component: ProdutosComponent }
];
```

HTML:

```html
<a routerLink="/produtos">Ver produtos</a>
<router-outlet></router-outlet>
```

---

## 11. Formulários

### Template-driven:
```html
<form #f="ngForm" (ngSubmit)="submit(f)">
  <input name="nome" ngModel required>
</form>
```

### Reactive Forms:

```ts
form = this.fb.group({
  nome: ['', Validators.required]
});
```

```html
<form [formGroup]="form" (ngSubmit)="submit()">
  <input formControlName="nome">
</form>
```

---

## 12. Requisições HTTP

Importe `HttpClientModule` em `app.module.ts`.

```ts
constructor(private http: HttpClient) {}

getProdutos() {
  return this.http.get('/api/produtos');
}
```

---

## 13. Ciclo de Vida dos Componentes

Principais hooks:
- `ngOnInit`
- `ngOnChanges`
- `ngOnDestroy`
- `ngAfterViewInit`

---

## 14. Módulos

Angular usa módulos para organizar a aplicação em partes reutilizáveis, escaláveis e com responsabilidades bem definidas.

### 📦 O que é um Módulo Angular?

Um módulo é uma classe decorada com `@NgModule`, que agrupa:
- Componentes
- Diretivas
- Pipes
- Serviços
- Outros módulos

### 🧱 Estrutura de um módulo:

```ts
@NgModule({
  declarations: [MeusComponentes],
  imports: [OutrosMódulos],
  exports: [ComponentesQueQueroReusar],
  providers: [ServiçosGlobaisOuLocais]
})
export class MeuModulo {}
```

### 🗂️ Pasta `modules`

A pasta `modules` serve para organizar melhor a aplicação. Exemplo de uso:

- `auth/` → tudo de login e autenticação
- `admin/` → páginas de administração
- `shared/` → componentes e serviços reutilizáveis

### 💡 Criar um módulo:

```bash
ng generate module nome
```

### 🔄 SharedComponentModule (Módulo Compartilhado)

Você pode (e deve) criar um módulo para componentes reutilizáveis, como botões, inputs, etc.

#### Exemplo:

```ts
@NgModule({
  declarations: [ButtonComponent, InputComponent],
  imports: [CommonModule, ReactiveFormsModule],
  exports: [ButtonComponent, InputComponent]
})
export class SharedComponentModule {}
```

### ✅ Como usar em outros módulos

```ts
import { SharedComponentModule } from '../components/shared-component.module';

@NgModule({
  imports: [SharedComponentModule]
})
export class PagesModule {}
```

### 📌 Resumo

| Elemento       | Para que serve                                                |
|----------------|---------------------------------------------------------------|
| `declarations` | Componentes, diretivas e pipes que pertencem a este módulo    |
| `imports`      | Outros módulos que este módulo precisa                        |
| `exports`      | O que será compartilhado com outros módulos                   |
| `providers`    | Serviços disponíveis para injeção de dependência              |

---

## 15. Guards e Rotas Protegidas

```bash
ng generate guard auth
```

Exemplo:

```ts
canActivate(): boolean {
  return this.authService.estaLogado();
}
```

---

## 16. Testes em Angular

Utiliza Jasmine e Karma.

Comando:

```bash
ng test
```

Testes ficam nos arquivos `.spec.ts`.

---

## 17. Build para Produção

```bash
ng build --prod
```

Gera a versão final otimizada na pasta `dist/`.

---

## 18. Boas Práticas

- Use módulos para organização
- Crie serviços para lógica reutilizável
- Evite lógica pesada no componente
- Utilize Reactive Forms em casos mais complexos
- Nomeie arquivos com clareza
- Use `async pipe` para lidar com observables
- Separe responsabilidades com `smart` e `dumb components`

---
