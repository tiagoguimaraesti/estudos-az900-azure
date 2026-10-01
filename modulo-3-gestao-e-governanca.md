# ☁️ Módulo 3: Gestão e Governação do Azure

## 1. Gestão de Custos no Azure

### Fatores que Afetam os Custos
*   **Tipo de Recurso e Configurações:** Uma VM com mais RAM e CPU custará mais. Além disso, o custo embute o preço da licença do Sistema Operativo (ex: Windows vs Linux)[cite: 49].
*   **Geografia:** O mesmo recurso pode ter preços diferentes em países distintos, devido a variações nos custos locais de energia e infraestrutura[cite: 51].
*   **Manutenção (Recursos Órfãos):** Ao excluir uma Máquina Virtual, o seu disco rígido e placa de rede **não** são apagados automaticamente[cite: 51]. Se os esquecer lá, continuará a pagar por esse armazenamento[cite: 51].
*   **Tráfego de Rede:** O tráfego de entrada (*Ingress* - para o Azure) é **gratuito**[cite: 51]. O tráfego de saída (*Egress* - do Azure para a internet) é **cobrado** com base em Zonas de Cobrança geográficas[cite: 51, 52].

### Modelos de Consumo (Como pagar)
| Modelo | Característica | Cenário Ideal |
| :--- | :--- | :--- |
| **Pay-as-you-go** | Paga apenas o que usa (tarifa cheia), sem compromisso[cite: 49]. | Picos variáveis ou sistemas imprevisíveis[cite: 49]. |
| **Reservations (Reservas)** | Contrato de 1 ou 3 anos para um servidor específico. Até 72% de desconto[cite: 49]. | Cargas de trabalho estáveis, bases de dados 24/7[cite: 49, 50]. |
| **Savings Plan** | Compromisso de 1 ou 3 anos baseado num valor de gasto por hora (ex: 5€/hora)[cite: 51]. | Exige flexibilidade de computação ao longo do tempo[cite: 51]. |
| **Spot Pricing** | Aluga capacidade ociosa dos datacenters com até 90% de desconto[cite: 51]. | Tarefas que podem ser interrompidas subitamente (ex: renderização)[cite: 51]. |

### Ferramentas de Previsão e Controlo
> **💡 Dica para a Prova:** A Microsoft adora confundir estas três!
> *   **Calculadora de Preços:** Estima custos **futuros** de novos recursos antes de os criar[cite: 52].
> *   **Calculadora TCO:** Compara custos para justificar a **migração** do ambiente físico local para a nuvem[cite: 52, 53].
> *   **Azure Cost Management:** Controla os gastos **atuais/passados**, cria orçamentos com alertas e ajuda a encontrar recursos ociosos para reduzir a fatura[cite: 53].

## 2. Organização com Tags
As *tags* (etiquetas) são pares de nome/valor (ex: `Departamento : RH`) utilizadas para organizar recursos para a faturação, gestão de operações e automação[cite: 54]. 
> **⚠️ Pulo do Gato:** As tags **NÃO são herdadas** automaticamente! Se colocar uma tag num Grupo de Recursos, os recursos dentro dele não a herdam por padrão[cite: 54].

## 3. Governação e Conformidade

### Microsoft Purview
É um "funil" inteligente de descoberta, classificação e rastreamento de dados sensíveis (ex: CPFs, cartões de crédito)[cite: 55]. A sua grande força é operar em ambientes **Multicloud** (AWS, GCP) e **On-premises**[cite: 55].

### Azure Policy
O Policy dita as regras da empresa e avalia continuamente se o ambiente está em conformidade[cite: 55, 56].
*   **Policy (Política):** Uma regra única (ex: "Exigir antivírus")[cite: 56].
*   **Initiative (Iniciativa):** Um "pacotão" que agrupa várias políticas para facilitar a gestão[cite: 56].
*   **Efeitos:** Pode bloquear criações indevidas (*Deny*), apenas avisar (*Audit*) ou até consertar o erro automaticamente (*Modify/Append - Auto-remediate*)[cite: 56].

### Resource Locks (Bloqueios de Recursos)
Funcionam como "cadeados" para evitar exclusões acidentais por erro humano[cite: 56]. 
*   **Delete Lock:** Permite ler e modificar, mas proíbe apagar[cite: 56].
*   **ReadOnly Lock:** Proíbe apagar e modificar. Só permite ler[cite: 56].
> **💡 Dica para a Prova:** O bloqueio é **soberano** e tem **herança automática**[cite: 56]. Mesmo um Administrador com permissão de *Owner* tem de remover o cadeado primeiro antes de conseguir apagar o recurso[cite: 56].
>
> ## 4. Segurança, Identidade e Defesa

### Confiança Zero (Zero Trust)
Abandona o antigo modelo de segurança baseado num "castelo e fosso" (onde a rede interna confiava em tudo). Os três princípios fundamentais são:
1.  **Verificar de modo explícito:** Autenticar e autorizar com base em pontos de dados (identidade, localização, saúde do dispositivo)[cite: 43].
2.  **Acesso com privilégio mínimo:** Utilizar o acesso just-in-time (JIT) e just-enough-access (JEA) através do RBAC[cite: 43].
3.  **Assumir violação:** Minimizar o impacto segmentando a rede para que um ataque não se propague livremente[cite: 43].

### Defesa em Profundidade
Estratégia de camadas sucessivas (como uma cebola) para proteger os dados. Nenhuma camada funciona isoladamente[cite: 44]:
*   *Segurança Física* $\rightarrow$ *Identidade e Acesso* $\rightarrow$ *Perímetro* $\rightarrow$ *Rede* $\rightarrow$ *Computação* $\rightarrow$ *Aplicação* $\rightarrow$ *Dados* (o alvo final)[cite: 44, 45].

### Criptografia e Azure Key Vault
*   **Em Repouso:** Protege os dados guardados (discos, bases de dados, storage) usando AES-256[cite: 45].
*   **Em Trânsito:** Protege os dados em movimento através de HTTPS, TLS e túneis VPN[cite: 45].
*   **Azure Key Vault:** O cofre centralizado que remove as credenciais (palavras-passe, *strings* de ligação e certificados) diretamente do código das aplicações[cite: 45, 46].

### Microsoft Defender para Nuvem
O "centro de comando" de segurança que avalia a postura (através de pontuações de segurança), protege os serviços e deteta ameaças em tempo real[cite: 47]. É multinuvem (suporta AWS e GCP) e protege ambientes locais através da integração com o **Azure Arc**[cite: 47].

## 5. Ferramentas de Interação com o Azure
*   **Portal do Azure:** Interface gráfica baseada no navegador (ideal para gestão visual e relatórios)[cite: 56, 57].
*   **Cloud Shell:** Terminal interativo baseado na web, já pré-configurado e autenticado (sem necessidade de instalação local)[cite: 56, 57].
*   **Azure PowerShell / CLI:** Linhas de comando para criar scripts e automatizar tarefas repetitivas (o PowerShell foca-se em comandos para Windows e a CLI em sintaxe estilo Bash/Linux)[cite: 56, 57].
*   **Azure Arc:** A extensão que permite gerir servidores e recursos que estão fora da Microsoft (noutras nuvens ou no teu datacenter local) utilizando exatamente o mesmo painel e regras do Azure[cite: 57, 58].

## 6. Arquitetura e Monitorização

### Azure Resource Manager (ARM)
O "maestro" central de todas as interações. Quer uses o portal, a CLI ou o PowerShell, o pedido passa obrigatoriamente pelo ARM para autenticação e orquestração[cite: 58]. Permite a **Infraestrutura como Código (IaC)** através de Modelos ARM (JSON) ou Bicep[cite: 58, 59].

### Azure Advisor
Analisa a tua configuração e emite recomendações gratuitas divididas em 5 pilares: *Confiabilidade, Segurança, Desempenho, Excelência Operacional e Custos* (sendo muito útil para detetar recursos ociosos que estão a gastar dinheiro)[cite: 59, 60].

### Estado do Serviço (Service Health)
*   **Azure Status:** Visão global e pública de todos os serviços no mundo[cite: 60].
*   **Service Health:** Visão personalizada do *teu* ambiente e regiões, avisando sobre manutenções programadas ou interrupções reais[cite: 60].
*   **Resource Health:** O diagnóstico focado num único recurso específico (ex: saber se uma VM caiu por falha da Microsoft ou por erro interno do sistema operativo)[cite: 60].

### Azure Monitor
A "caixa-preta" e painel de instrumentos do ambiente. Recolhe métricas (números rápidos) e logs (registos detalhados), permitindo criar **Alertas** e acionar o dimensionamento automático (**Autoscale**)[cite: 61]. O **Application Insights** foca-se em monitorizar o desempenho interno de aplicações e sites web.
