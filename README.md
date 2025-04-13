# 💻 Trabalho de Sistemas Operacionais – Parte 2  
## Tema: Concorrência e Mecanismos de Sincronização  

### 👥 Alunos
- Davi Gledson da Silva Benedito  
- Ana Kelry Fernandes Cabral do Nascimento  
- Bruno Eduardo Costa da Silva  
- João Heitor de Oliveira Morais  
- Gabriel Oliveira Silva  

**Professora:** Jéssica Figueiredo  

---

## 🎯 Objetivo  
Desenvolver uma solução visual e funcional para o problema clássico de concorrência conhecido como **"Jantar dos Filósofos"**, utilizando mecanismos de sincronização como **semáforos, mutex** e controle de estado.  
A solução foi implementada em **Python**, com interface gráfica utilizando **Tkinter**.

---

## ⚙️ Escolhas de Implementação  

### 📌 Linguagem: Python 3  
A escolha por Python se deu por ser uma linguagem de alto nível, de fácil leitura, ampla comunidade e suporte robusto a bibliotecas para desenvolvimento tanto de interfaces gráficas quanto de programas com múltiplas threads. Além disso, permite prototipagem rápida e integração simples com recursos gráficos via Tkinter.

### 🖼️ Interface Gráfica: Tkinter  
Tkinter é a biblioteca padrão do Python para criação de interfaces gráficas (GUI). Foi utilizada para criar uma interface visual que mostra:
- O estado de cada filósofo através de **círculos coloridos** (pensando, faminto, comendo)
- **Botões de início da simulação** e de **visualização da solução**
- Um **contador de refeições por filósofo**

Tkinter facilita o controle de eventos com botões, atualização visual em tempo real com `Canvas`, e integração com as threads que simulam os filósofos.

---

### 🧵 Concorrência: `threading.Thread`  
A biblioteca `threading` do Python permite criar **threads independentes** de execução.  
Cada filósofo é representado por uma thread separada, o que simula o comportamento concorrente típico dos problemas de sistemas operacionais.

Cada thread executa um ciclo onde o filósofo:
- Pensa por um tempo aleatório
- Fica faminto e tenta pegar os garfos
- Come (se possível)
- Devolve os garfos e reinicia o ciclo

Isso representa o modelo real de **múltiplos processos concorrendo por recursos**.

---

### 🔐 Sincronização

#### 🔒 `threading.Lock` – Exclusão Mútua (Mutex)  
Utilizado como **mutex global**, garantindo que **apenas uma thread por vez** possa alterar os estados dos filósofos ou acessar os garfos.  
Evita **condições de corrida** durante alterações críticas como:
- Mudança de estado para "faminto" ou "comendo"
- Liberação dos garfos após comer

#### 🚦 `threading.Semaphore` – Controle Individual  
Cada filósofo possui um **semáforo próprio**. Isso permite bloquear ou liberar um filósofo individualmente quando ele tenta comer, garantindo o acesso coordenado aos recursos.

---

## 🧠 Funcionamento da Solução

A interface representa visualmente os cinco filósofos e seus estados.  
Cada filósofo pode estar em:

- 🟡 **Pensando**: Círculo amarelo  
- 🔴 **Faminto**: Círculo vermelho  
- 🟢 **Comendo**: Círculo verde  

Cada filósofo possui um **contador de refeições** realizado, exibido abaixo de seu nome.

### 🔘 Botões disponíveis:
- **"Iniciar Simulação"**: dispara a execução das threads dos filósofos  
- **"Mostrar Solução"**: exibe uma janela explicando a estratégia adotada para evitar deadlock e starvation

---

## 🔄 Lógica de Sincronização

A estratégia adotada garante que os filósofos **só comam quando seus vizinhos não estiverem comendo**.  
Isso é feito por meio da função `testar(i)` que verifica o estado dos vizinhos.

### Componentes principais:
- `estado[]`: lista com o estado de cada filósofo (pensando, faminto, comendo)  
- `semaforos[]`: semáforo individual por filósofo para controlar acesso aos "garfos"  
- `mutex`: trava global usada para garantir que apenas um filósofo altere estados por vez

### Etapas do ciclo de cada filósofo:
1. **Pensar**: espera por um tempo aleatório  
2. **Ficar faminto**: tenta adquirir os garfos  
3. **Comer**: se os vizinhos não estão comendo, entra na seção crítica  
4. **Devolver garfos**: altera estado e verifica se os vizinhos podem comer

Essa abordagem evita **deadlock** (travamento) e **starvation** (fome infinita de algum filósofo), promovendo **justiça no acesso aos recursos**.

---

## ✅ Resultados  

A simulação visual mostra claramente os ciclos de **pensamento**, **fome** e **alimentação**.  
O **contador de refeições** comprova que todos os filósofos participam da execução sem bloqueios injustos.  
O botão **"Mostrar Solução"** facilita a **compreensão teórica da estratégia de sincronização** adotada.

---

## 🧾 Conclusão  

O trabalho implementa com sucesso um exemplo clássico de concorrência e sincronização em sistemas operacionais.  
Demonstra, de forma interativa e didática, como **mutex e semáforos** podem ser utilizados para resolver problemas de acesso simultâneo a recursos compartilhados.

A solução reforça conceitos fundamentais de SO como:
- Deadlock  
- Starvation  
- Exclusão mútua  
- Justiça no acesso  

---

## 📚 Referências  

- Silberschatz, A., Galvin, P. B., & Gagne, G. (2018). *Operating System Concepts*  
- [Documentação oficial do Python](https://docs.python.org/3/)  
- Material didático da disciplina  
- [O Jantar dos Filósofos - Blog Pantuza](https://blog.pantuza.com/artigos/o-jantar-dos-filosofos-problema-de-sincronizacao-em-sistemas-operacionais)
