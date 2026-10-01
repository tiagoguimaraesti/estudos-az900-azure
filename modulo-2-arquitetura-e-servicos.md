# ☁️ Módulo 2: Arquitetura e Principais Serviços do Azure

## 1. Categorias de Serviços (Os Quatro Pilares)
*   **Compute (Computação):** O "cérebro" e os músculos. Onde aluga poder de processamento. (Ex: *Virtual Machines, App Service, Azure Functions*).
*   **Networking (Redes):** As estradas e túneis que conectam os servidores e a internet. (Ex: *Virtual Network/VNet, ExpressRoute*).
*   **Storage (Armazenamento):** O "disco rígido" gigante para guardar arquivos soltos e estruturados. (Ex: *Blob Storage, Azure Files*).
*   **Databases (Bancos de Dados):** Onde guarda os dados estruturados e organizados da empresa. (Ex: *Azure SQL, Cosmos DB*).

## 2. Estrutura e Hierarquia de Organização
O Azure organiza tudo como um sistema de pastas, fluindo do maior para o menor:

1.  **Grupo de Gerenciamento (Management Group):** O nível mais alto, que agrupa assinaturas para aplicar regras de governação e segurança em massa.
2.  **Assinatura (Subscription):** A fronteira de **faturação** e controlo de acesso. Pode-se ter várias assinaturas na mesma conta (ex: uma para a equipa de *Dev* e outra para o sistema em *Produção*).
3.  **Grupos de Recursos (Resource Groups):** São as pastas organizadoras lógicas. Um recurso precisa de morar obrigatoriamente dentro de um único Grupo de Recursos. Não podem ser aninhados (colocar um grupo dentro do outro).
4.  **Recursos (Resources):** A "mão na massa". As Máquinas Virtuais, as bases de dados, as redes, etc.

> **💡 Dica para a Prova:**
> **A Lei da Herança e Cascata:** As regras e permissões fluem de cima para baixo. Se você apagar um Grupo de Recursos, TODOS os recursos que estão dentro dele são apagados instantaneamente de uma só vez!

## 3. Infraestrutura Física e Zonas
*   **Geografia:** O país ou mercado (Ex: Brasil). Garante a residência de dados para cumprir leis locais (como a LGPD).
*   **Região:** Um conjunto de datacenters próximos, conectados por uma rede de fibra ótica de baixa latência. 
*   **Zona de Disponibilidade (Availability Zone):** São "bairros" diferentes dentro de uma região, com energia, internet e refrigeração independentes, garantindo proteção se um datacenter inteiro falhar.

| Tipo de Serviço | Como Funciona na Prática | Exemplo Típico |
| :--- | :--- | :--- |
| **Zonal** | Fica preso numa zona específica (Se a zona falhar, o serviço cai). | Máquinas Virtuais (VMs) |
| **Redundante de Zona** | O Azure espalha cópias automaticamente entre 3 zonas distintas. | Banco de Dados SQL |
| **Global (Não-Regional)** | Funciona no mundo todo, não dependendo de uma infraestrutura local. | Microsoft Entra ID |

> **💡 Dica para a Prova:**
> **Pares de Regiões (Region Pairs):** O Azure organiza as regiões em pares a pelo menos 480 km de distância (ex: Brasil Sul faz par com Centro-Sul dos EUA). Se houver atualizações de sistema, a Microsoft nunca atualiza o par ao mesmo tempo, garantindo que pelo menos um esteja sempre online.
>
> ## 4. Serviços de Computação do Azure

### Máquinas Virtuais (VMs)
*   **O que são:** Servidores virtualizados (IaaS) onde tens controlo total sobre o sistema operativo[cite: 23]. Ideais para migrações *lift-and-shift* e cenários de teste/desenvolvimento.
*   **Famílias de VMs Principais:** 
    *   **Série D:** Utilização Geral (Equilíbrio entre CPU e memória).
    *   **Série E:** Otimizadas para Memória (Excelentes para grandes bases de dados).
    *   **Série F:** Otimizadas para Computação (Processamento pesado de CPU).
*   **Scale Sets (VMSS):** Agrupamento inteligente que escala (aumenta ou diminui) a quantidade de Máquinas Virtuais idênticas de forma automática, conforme a exigência de tráfego.
*   **Conjuntos de Disponibilidade:** Protegem as VMs contra quedas distribuindo-as por *Domínios de Atualização* (proteção contra manutenções agendadas pela Microsoft) e *Domínios de Falha* (proteção contra falhas de hardware ou energia no *rack*).

### Azure Virtual Desktop (AVD)
Solução de virtualização de ambiente de trabalho na nuvem.
*   Ideal para trabalhadores remotos, modelos híbridos ou dispositivos próprios (BYOD).
*   **Diferencial:** Permite sessões múltiplas (*multi-session*) no Windows, reduzindo drasticamente os custos ao partilhar a mesma Máquina Virtual por vários utilizadores em simultâneo.

### Contentores (Containers) e Computação Sem Servidor
*   **Contentores:** Ambientes leves que empacotam apenas a aplicação e as suas dependências, partilhando o sistema operativo base do servidor anfitrião. Iniciam em segundos e oferecem grande portabilidade.
    *   **ACI (Azure Container Instances):** A forma mais simples, rápida e direta de executar um contentor isolado (PaaS).
    *   **AKS (Azure Kubernetes Service):** Serviço de orquestração avançado para gerir "frotas" gigantes de contentores a nível empresarial.
*   **Azure Functions (Serverless):** Computação controlada por eventos. Não geres infraestrutura; o código só é ativado por "gatilhos" (ex: um clique, um horário) e pagas estritamente pelo tempo exato de processamento (milissegundos).

## 5. Serviços de Rede do Azure

### Redes Virtuais (VNets) e Segurança
*   **VNet:** O limite físico do teu ambiente na nuvem. Pode ser dividida em **sub-redes** para isolar diferentes partes do sistema (ex: servidores web separados de bases de dados).
*   **NSG (Grupo de Segurança de Rede):** O teu primeiro filtro de segurança[cite: 30]. Bloqueia ou permite tráfego com base em regras rápidas de IP e porta de entrada/saída.
*   **NVA (Aplicação Virtual de Rede):** Uma Máquina Virtual especializada (como firewalls avançadas) que faz inspeção profunda de pacotes e deteção de intrusões.
*   **VNet Peering:** Conecta redes virtuais diferentes (mesmo noutras regiões do globo)[cite: 30]. O tráfego viaja exclusivamente pela rede privada (backbone) da Microsoft, garantindo segurança e baixa latência sem passar pela internet[cite: 30].

### Conectividade Híbrida (Ligar a Empresa à Nuvem)
*   **VPN Ponto a Site (Point-to-Site):** Túnel seguro de um dispositivo individual (ex: o portátil do teu utilizador remoto) para o Azure.
*   **VPN Site a Site (Site-to-Site):** Conecta o router físico da sede da empresa ao Gateway do Azure através da internet criptografada.
*   **ExpressRoute:** Conexão dedicada de fibra ótica diretamente para a Microsoft. É extremamente rápida, fiável e **não utiliza a internet pública**.

> **💡 Dica para a Prova:**
> Se o cenário da certificação mencionar que a política de segurança da empresa "proíbe estritamente o trânsito pela internet pública", a resposta correta será **ExpressRoute**. O recurso **ExpressRoute Global Reach** permite até ligar duas filiais físicas entre si utilizando apenas a rede interna da Microsoft.
>
> ## 6. Azure DNS
*   **Hospedagem e Roteamento Anycast:** O Azure DNS não compra domínios, mas hospeda os seus registos[cite: 34]. Utiliza o roteamento *Anycast*, que direciona o utilizador para o servidor DNS fisicamente mais próximo e saudável, garantindo uma latência baixíssima a nível global.
*   **Registos de Alias:** Apontam diretamente para recursos do Azure (como um Balanceador de Carga) em vez de um IP fixo. Se o IP mudar nos bastidores, o registo atualiza-se sozinho, evitando tempo de inatividade (downtime).

## 7. Contas de Armazenamento do Azure (Storage)
O nome da conta deve ser globalmente único e conter apenas letras minúsculas e números (3 a 24 caracteres). A conta Standard suporta quatro serviços principais:
*   **Blobs:** Para ficheiros pesados, não estruturados (fotos, vídeos, backups) e Big Data (Data Lake).
*   **Files (Ficheiros):** Partilhas de rede locais na nuvem, suportando protocolos SMB e NFS.
*   **Queues (Filas):** Armazena milhões de mensagens curtas para comunicação entre aplicações.
*   **Tables (Tabelas):** Base de dados estruturada NoSQL, rápida e barata.

### Redundância de Armazenamento (Proteção de Dados)
*   **LRS (Local):** 3 cópias no mesmo datacenter. Protege contra falha de um disco, mas não do prédio.
*   **ZRS (Zona):** 3 cópias espalhadas por 3 zonas (prédios) diferentes na mesma região
*   **GRS (Geográfica):** 3 cópias locais + 3 cópias numa região secundária a centenas de quilómetros de distância (proteção máxima contra desastres regionais).

## 8. Migração e Movimentação de Dados

### Ferramentas de Migração
*   **Azure Migrate:** Ferramenta online (hub centralizado) para avaliar e migrar infraestrutura local (servidores, bases de dados) em tempo real para a nuvem. Ideal para estratégias *Lift and Shift*.
*   **Azure Data Box:** Solução física (offline)[cite: 37]. Se a internet for muito lenta para transferir dezenas de Terabytes, a Microsoft envia um equipamento (disco rígido seguro) por transportadora para a sua empresa fazer a cópia localmente.

### Ferramentas de Movimentação do Dia a Dia
| Ferramenta | Característica Principal | Cenário Ideal |
| :--- | :--- | :--- |
| **AzCopy** | Linha de comandos (Rápido e Unidirecional)[cite: 38]. | Scripts automatizados ou envio massivo via terminal. |
| **Storage Explorer** | Aplicação visual (Interface Gráfica)[cite: 38]. | Gestão manual, arrastar e largar ficheiros (usa o AzCopy nos bastidores). |
| **Azure File Sync** | Agente de sincronização bidirecional[cite: 38]. | Manter servidores de ficheiros locais sempre atualizados com a nuvem (*Cloud tiering*). |
