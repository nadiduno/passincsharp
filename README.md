[![Author](https://img.shields.io/badge/Dev-Nadi%20Duno-blueviolet%20)](https://portfolio-nadi.vercel.app/)
[![Social](https://img.shields.io/twitter/follow/nadiduno?label=%40nadiduno&style=social)](https://twitter.com/nadiduno)
[![Linkedin](https://img.shields.io/badge/in-Nadi%20Duno-blue)](https://www.linkedin.com/in/nadiduno/)
<br />
<br />
#PassIn

Aplicação back-end em C# com .NET documentação da API com Swagger

![Technologies](https://img.shields.io/badge/%3C%2F%3E-technologies-lightgrey)<br/>
[C#](https://learn.microsoft.com/pt-br/dotnet/csharp/language-reference/language-specification/documentation-comments) | [SQLite](https://www.sqlite.org/) | [Swagger](https://swagger.io/) | [Entity Framework](https://learn.microsoft.com/en-us/ef/core/)

<br />
#Requisitos
##Requisitos funcionais

    O organizador deve poder cadastrar um novo evento;
    O organizador deve poder visualizar dados de um evento;
    O organizador deve poser visualizar a lista de participantes;
    O participante deve poder se inscrever em um evento;
    O participante deve poder visualizar seu crachá de inscrição;
    O participante deve poder realizar check-in no evento;

##Regras de negócio

    O participante só pode se inscrever em um evento uma única vez;
    O participante só pode se inscrever em eventos com vagas disponíveis;
    O participante só pode realizar check-in em um evento uma única vez;

##Requisitos não-funcionais

    O check-in no evento será realizado através de um QRCode;

## Banco de dados
Nessa aplicação vamos utilizar banco de dados relacional (SQL). Para ambiente de desenvolvimento seguiremos com o SQLite pela facilidade do ambiente.

##Documentação da API (Swagger)
<br />

<div>
  <img 
    alt="Documentação da API com Swagger"
    src="https://github.com/nadiduno/passincsharp/blob/main/.github/ImgApp.png" 
    width="70%"
  >
  <br />
</div>

 ```
-- CreateTable
CREATE TABLE "events" (
    "id" TEXT NOT NULL PRIMARY KEY,
    "title" TEXT NOT NULL,
    "details" TEXT,
    "slug" TEXT NOT NULL,
    "maximum_attendees" INTEGER
);

-- CreateTable
CREATE TABLE "attendees" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "event_id" TEXT NOT NULL,
    "created_at" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT "attendees_event_id_fkey" FOREIGN KEY ("event_id") REFERENCES "events" ("id") ON DELETE RESTRICT ON UPDATE CASCADE
);

-- CreateTable
CREATE TABLE "check_ins" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "created_at" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "attendeeId" INTEGER NOT NULL,
    CONSTRAINT "check_ins_attendeeId_fkey" FOREIGN KEY ("attendeeId") REFERENCES "attendees" ("id") ON DELETE RESTRICT ON UPDATE CASCADE
);

-- CreateIndex
CREATE UNIQUE INDEX "events_slug_key" ON "events"("slug");

-- CreateIndex
CREATE UNIQUE INDEX "attendees_event_id_email_key" ON "attendees"("event_id", "email");

-- CreateIndex
CREATE UNIQUE INDEX "check_ins_attendeeId_key" ON "check_ins"("attendeeId");
````

By DevRel 💜 [Nadi Duno](https://www.linkedin.com/in/nadiduno/) © 2024
<br />
<br />

Este é meu [Diario de estudo](https://devrelnadiduno.blogspot.com/) 
<br />
<br />

[Link do Potfólio](https://portfolionadiduno.vercel.app/) 
