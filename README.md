
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

Transformações no template:

```html
{{ preco | currency:'BRL' }}
{{ data | date:'dd/MM/yyyy' }}
```

Custom pipe:

```bash
ng generate pipe nome
```

---

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

Angular usa módulos para organizar a aplicação.

Criação:

```bash
ng generate module nome
```

Importação:

```ts
@NgModule({
  imports: [CommonModule],
  declarations: [MeuComponente]
})
export class MeuModulo {}
```

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

