# ☁️ Módulo 1: Descrever Conceitos de Nuvem

## 1. O que é a Computação em Nuvem?
A computação em nuvem é a entrega de serviços de computação pela Internet. Altera o planeamento de infraestrutura, passando de longos ciclos de aquisição para o provisionamento imediato. As equipas podem testar e adaptar a capacidade rapidamente à medida que os requisitos mudam.

## 2. O Modelo de Responsabilidade Partilhada
O nível de gestão varia conforme o modelo escolhido. Numa extremidade, o **IaaS** coloca a maior responsabilidade sobre o consumidor, enquanto o **SaaS** coloca a maior parte com o provedor (Microsoft). 

| Área de Responsabilidade | Local (On-Premises) | IaaS | PaaS | SaaS |
| :--- | :--- | :--- | :--- | :--- |
| **Dados e Informações** | Cliente | Cliente | Cliente | Cliente |
| **Aplicações** | Cliente | Cliente | Partilhado | Partilhado |
| **Sistema Operativo** | Cliente | Cliente | Microsoft | Microsoft |
| **Rede Física e Datacenter** | Cliente | Microsoft | Microsoft | Microsoft |

> **💡 Dica para a Prova:**
> **O que fica SEMPRE com o cliente:** As contas, as identidades, os dispositivos (endpoints) e os dados armazenados.
> **O que fica SEMPRE com o provedor:** O datacenter físico, a rede física e os hosts físicos.

## 3. Modelos de Implantação de Nuvem
A forma como os recursos de nuvem são implantados define o modelo de nuvem.

*   **Nuvem Pública:** O provedor é dono da infraestrutura física. Você acessa via internet e paga pelo que usa (OpEx). Não há controle físico.
*   **Nuvem Privada:** Você tem controlo total sobre os recursos e a segurança. Exige compra de hardware (CapEx) e manutenção própria.
*   **Nuvem Híbrida:** Mistura o ambiente local (on-premises) com a nuvem pública, oferecendo maior flexibilidade para manter dados confidenciais localmente e escalar outras aplicações na nuvem.
*   **Multinuvem (Multicloud):** Utilização de dois ou mais provedores de nuvem pública (ex: Azure e AWS) simultaneamente.

> **💡 Dica para a Prova:**
> **Azure Arc:** É o "comando universal". Permite gerir recursos (servidores, Kubernetes) que estão na sua empresa ou na concorrência (AWS/Google) usando o mesmo painel do Azure.
> **Solução VMware no Azure:** Permite migrar a infraestrutura VMware local inteira para os datacenters da Microsoft sem ter de reescrever sistemas.

## 4. O Modelo Baseado em Consumo (OpEx vs CapEx)
A computação em nuvem abandona as **Despesas de Capital (CapEx)** — gastos iniciais com infraestrutura física — e passa para **Despesas Operacionais (OpEx)**, onde se paga apenas pelo que se consome ao longo do tempo.
*   Não há custos iniciais com datacenters.
*   Paga-se apenas pela capacidade utilizada, eliminando desperdícios de servidores inativos.

## 5. Benefícios da Nuvem (O Core da AZ-900)

### Alta Disponibilidade (SLA - Service Level Agreement)
Garante o tempo mínimo de funcionamento do sistema. Obter mais "noves" (ex: passar de 99,9% para 99,99%) exige arquiteturas mais complexas e redundantes, o que aumenta o custo financeiro[cite: 9].
*   **99% (2 noves):** Pode ficar fora do ar ~7,3 horas por mês[cite: 9].
*   **99,9% (3 noves):** Pode ficar fora do ar ~44 minutos por mês[cite: 10].
*   **99,99% (4 noves):** Pode ficar fora do ar apenas ~4 minutos por mês (Alta excelência)[cite: 9, 10].

### Escalabilidade
Ajuste de recursos para corresponder à demanda de tráfego[cite: 11].
*   **Escalonamento Vertical (Scale Up/Down):** Aumentar a "força" da mesma Máquina Virtual (adicionar CPU e RAM)[cite: 10]. Exige reinício (downtime)[cite: 10].
*   **Escalonamento Horizontal (Scale Out/In):** Adicionar a "quantidade" de Máquinas Virtuais para dividir o trabalho[cite: 10]. É o superpoder da nuvem, feito sem interrupção do sistema[cite: 10].

### Confiabilidade e Previsibilidade
*   **Confiabilidade:** Capacidade do sistema se recuperar de falhas graves[cite: 11]. Utiliza o conceito de *Failover* (redirecionamento de tráfego) e *Pares de Regiões* para sobreviver a desastres naturais que destruam uma região inteira do Azure[cite: 11].
*   **Previsibilidade:** Garantida através de ferramentas de performance (Autoscaling, Balanceamento de Carga) e de custos (Azure Cost Management, Calculadora de Preços)[cite: 12].

### Segurança e Governança
*   **Governança:** Definir e atualizar padrões em escala (Templates)[cite: 12].
*   **Conformidade:** Auditoria 24h e aplicação de patches/manutenção automática[cite: 13].
*   **Segurança:** Proteções integradas (como bloqueio contra DDoS) que seriam extremamente caras de manter num datacenter local[cite: 13].

### Gestão NA Nuvem vs. Gestão DA Nuvem
> **⚠️️ Pulo do Gato:** A banca adora confundir estes dois conceitos!
> *   **Gestão DA nuvem:** Auto-scale, monitorização da integridade (Health Monitor), Alertas automáticos. É o Azure a trabalhar para si de forma invisível[cite: 13, 14].
> *   **Gestão NA nuvem:** O que você usa para interagir: Portal do Azure (Visual), PowerShell (Scripts via Windows), CLI (Scripts via Bash/Linux) e APIs (acesso programático)[cite: 14]. Todos eles passam obrigatoriamente pelo *Azure Resource Manager (ARM)*[cite: 14].

## 6. Sustentabilidade
O Azure ajuda a reduzir a pegada de carbono operacionalizando a eficiência[cite: 14].
1.  **Monitorar:** Acompanhar recursos ociosos[cite: 14].
2.  **Right-size (Dimensionamento correto):** Adequar servidores gigantes à demanda real[cite: 14].
3.  **Automatizar:** Desligar recursos fora do horário de trabalho automaticamente[cite: 14, 15].
4.  **Otimizar:** Mudar para serviços mais modernos e eficientes energeticamente (como Serverless)[cite: 15].

## 7. Tipos de Serviço de Nuvem (IaaS, PaaS, SaaS)

| Modelo | O que a Microsoft gere | O que você gere | Cenários Ideais de Prova |
| :--- | :--- | :--- | :--- |
| **IaaS** | Hardware físico e rede[cite: 15] | S.O., aplicações, dados, atualizações[cite: 15] | Migrações *Lift-and-shift*; Ambientes de teste e desenvolvimento. Maior controlo[cite: 15, 16]. |
| **PaaS** | Hardware, S.O., Middleware, Runtime[cite: 16] | Aplicações e Dados[cite: 16] | Desenvolvimento rápido de *frameworks* sem gerir servidores; Análise de Dados (BI). Modelo equilibrado[cite: 16, 17]. |
| **SaaS** | Toda a infraestrutura e aplicação[cite: 17] | Dados de acesso (Login/Senha)[cite: 17] | Microsoft 365, e-mail corporativo, sistemas financeiros. Menor controlo de TI[cite: 17, 18]. |
