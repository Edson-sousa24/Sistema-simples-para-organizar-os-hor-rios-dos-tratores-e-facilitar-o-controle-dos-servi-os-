

### Q1: Existe algum estabelecimento/associação/pessoa/instituição que precisaria de um sistema web? Caso sim, descreva.

Sim. O Grupo Sousa Tratores e Serviços é uma empresa que presta serviços utilizando máquinas e tratores agrícolas. Para realizar esses serviços, é necessário organizar informações como clientes, datas, horários, tipo de serviço, trator utilizado e quantidade de horas contratadas.

Atualmente, essas informações podem ser controladas de maneira manual, por meio de anotações, mensagens ou planilhas, o que pode dificultar a organização dos horários dos tratores e o acompanhamento dos serviços.

Dessa forma, foi escolhido o desenvolvimento de um sistema web simples para agendamento de horas de tratores, permitindo centralizar essas informações em uma única aplicação.

### Q2: Quais são as principais consequências e impactos causados pelo problema? Como o sistema web solucionaria ou ajudaria a resolver os impactos?

A falta de um sistema específico para organizar os agendamentos pode causar alguns problemas, como:

dificuldade para visualizar os horários já reservados;
possibilidade de esquecer ou duplicar agendamentos;
dificuldade para organizar os serviços dos tratores;
perda de informações sobre clientes e serviços;
dificuldade para saber quantas horas foram contratadas;
maior dependência de anotações manuais;
dificuldade para consultar rapidamente os serviços programados.

O sistema web ajudará a reduzir esses problemas ao permitir que os dados sejam registrados de forma organizada.

Por meio do sistema, o responsável poderá informar o cliente, data, horário, serviço, trator e quantidade de horas. Após o cadastro, essas informações serão apresentadas em uma tabela de agendamentos, facilitando a visualização e o controle dos serviço

# Q3: Como seria o protótipo da solução? Que tipo de informação o sistema web deveria conter? Como essas informações poderiam ser organizadas no website?

O protótipo consiste em um sistema web desenvolvido para o Grupo Sousa Tratores e Serviços, com o objetivo de facilitar o agendamento e a organização das horas de trabalho dos tratores. O sistema possui um formulário para cadastro de cliente, data, horário, serviço, trator e quantidade de horas. Após o cadastro, os dados são apresentados em uma tabela, permitindo uma visualização organizada dos agendamentos. A primeira versão utiliza React, HTML e CSS, podendo futuramente receber recursos como banco de dados, login, calendário, cadastro de clientes e tratores, valores dos serviços e relatórios.

# Sistema-simples-para-organizar-os-hor-rios-dos-tratores-e-facilitar-o-controle-dos-servi-os-
Disciplina web1[README.md](https://github.com/user-attachments/files/32559649/README.md)

# Grupo Sousa Tratores e Serviços — Parte 1

## Objetivo
Criar uma primeira versão simples de um sistema web para agendamento de horas de tratores.

## O que a Parte 1 possui
- Logo do Grupo Sousa;
- formulário de agendamento;
- cliente;
- data;
- horário;
- serviço;
- trator;
- quantidade de horas;
- tabela com os agendamentos;
- layout simples e responsivo;
- React, HTML e CSS;
- componentes React;
- Flexbox no formulário e no cabeçalho.

## Como executar

No VS Code, abra esta pasta e execute:

```bash
npm.cmd install
npm.cmd run dev -- --host 0.0.0.0
```

Depois abra o endereço informado pelo Vite, normalmente:

```text
http://localhost:5173
```

## Parte 2 — próximo semestre
A segunda etapa poderá evoluir este projeto com:
- banco de dados;
- login;
- cadastro de clientes;
- cadastro de tratores;
- cadastro de operadores;
- calendário;
- confirmação/cancelamento;
- cálculo de valor por hora;
- ordem de serviço;
- relatórios;
- publicação online.

A ideia é manter a Parte 1 pequena e funcional, criando uma base para expansão futura.
[style.css](https://github.com/user-attachments/files/32559742/style.css)

import React, { useState } from "react";
import { createRoot } from "react-dom/client";
import "./style.css";

function Header() {
  return (
    <header className="header">
      <img src="/logo-grupo-sousa.png" alt="Grupo Sousa Tratores e Serviços" />
      <div>
        <h1>Agendamento de Tratores</h1>
        <p>Grupo Sousa Tratores e Serviços</p>
      </div>
    </header>
  );
}

function AgendamentoForm({ onAdicionar }) {
  const [form, setForm] = useState({
    cliente: "",
    data: "",
    hora: "",
    servico: "Gradagem",
    trator: "Trator 01",
    horas: ""
  });

  function mudar(campo, valor) {
    setForm({ ...form, [campo]: valor });
  }

  function enviar(e) {
    e.preventDefault();

    if (!form.cliente || !form.data || !form.hora || !form.horas) {
      alert("Preencha cliente, data, horário e quantidade de horas.");
      return;
    }

    onAdicionar(form);

    setForm({
      cliente: "",
      data: "",
      hora: "",
      servico: "Gradagem",
      trator: "Trator 01",
      horas: ""
    });
  }

  return (
    <section className="box">
      <h2>Novo agendamento</h2>

      <form onSubmit={enviar}>
        <label>
          Cliente
          <input
            type="text"
            value={form.cliente}
            onChange={(e) => mudar("cliente", e.target.value)}
            placeholder="Nome do cliente"
          />
        </label>

        <label>
          Data
          <input
            type="date"
            value={form.data}
            onChange={(e) => mudar("data", e.target.value)}
          />
        </label>

        <label>
          Horário
          <input
            type="time"
            value={form.hora}
            onChange={(e) => mudar("hora", e.target.value)}
          />
        </label>

        <label>
          Serviço
          <select
            value={form.servico}
            onChange={(e) => mudar("servico", e.target.value)}
          >
            <option>Gradagem</option>
            <option>Plantio</option>
            <option>Aração</option>
            <option>Roçagem</option>
            <option>Sulcamento</option>
            <option>Colheita</option>
          </select>
        </label>

        <label>
          Trator
          <select
            value={form.trator}
            onChange={(e) => mudar("trator", e.target.value)}
          >
            <option>Trator 01</option>
            <option>Trator 02</option>
          </select>
        </label>

        <label>
          Quantidade de horas
          <input
            type="number"
            min="1"
            step="0.5"
            value={form.horas}
            onChange={(e) => mudar("horas", e.target.value)}
            placeholder="Ex.: 4"
          />
        </label>

        <button type="submit">Agendar</button>
      </form>
    </section>
  );
}

function Agenda({ agendamentos }) {
  return (
    <section className="box">
      <h2>Agendamentos</h2>

      {agendamentos.length === 0 ? (
        <p className="vazio">Nenhum agendamento cadastrado.</p>
      ) : (
        <div className="tabela">
          <table>
            <thead>
              <tr>
                <th>Cliente</th>
                <th>Data</th>
                <th>Hora</th>
                <th>Serviço</th>
                <th>Trator</th>
                <th>Horas</th>
              </tr>
            </thead>
            <tbody>
              {agendamentos.map((item) => (
                <tr key={item.id}>
                  <td>{item.cliente}</td>
                  <td>{item.data}</td>
                  <td>{item.hora}</td>
                  <td>{item.servico}</td>
                  <td>{item.trator}</td>
                  <td>{item.horas} h</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}
    </section>
  );
}

function App() {
  const [agendamentos, setAgendamentos] = useState([]);

  function adicionar(item) {
    setAgendamentos([
      ...agendamentos,
      { ...item, id: Date.now() }
    ]);
  }

  return (
    <>
      <Header />

      <main className="container">
        <section className="apresentacao">
          <h2>Parte 1 — Agendamento de Horas</h2>
          <p>
            Sistema simples para organizar os horários dos tratores e facilitar
            o controle dos serviços realizados pelo Grupo Sousa.
          </p>
        </section>

        <AgendamentoForm onAdicionar={adicionar} />
        <Agenda agendamentos={agendamentos} />

        <section className="futuro">
          <strong>Próxima etapa:</strong>
          banco de dados, login, calendário, cadastro de clientes e tratores,
          valores dos serviços e relatórios.
        </section>
      </main>

      <footer>
        Grupo Sousa Tratores e Serviços — Programação Web I
      </footer>
    </>
  );
}

createRoot(document.getElementById("root")).render(<App />);


