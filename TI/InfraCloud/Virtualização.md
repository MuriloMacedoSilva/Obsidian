A virtualização no contexto de DevOps é um dos pilares que viabilizam a infraestrutura ágil, a automação e a cultura de entrega contínua (CI/CD). Em termos simples, ela elimina o gargalo do "na minha máquina funciona", permitindo que desenvolvedores e engenheiros de operações criem, testem e distribuam aplicações em ambientes idênticos e isolados, independentemente do hardware físico subjacente.

Para entender a fundo, precisamos dividir esse conceito em como ele funciona estruturalmente e quais são os seus dois grandes modelos: **Virtualização de Hardware (VMs)** e **Virtualização de Sistema Operacional (Containers)**.

# Como Funciona a Virtualização?

O principio base da virtualização é a abstração. Uma camada de software intercepta as requisições que o sistema operacional faria diretamente ao hardware físico (Processador, Memória RAM, Armazenamento, Rede) e as distribui de forma isolada.

## 1. Virtualização Tradicional (Baseada em Hipervisor / VMs)

Neste modelo, utilizamos um software chamado Hypervisor (ou Mnitor de Máquina Virtual) para fatiar um servidor físico em múltiplas Máquinas Virtuais (VMs). Cada VM funciona como um computador completo independente.

- Hipervisor Tipo 1 (Bare-Metal) : Roda diretamente no hardware físico (ex: VMware ESXI, KVM). É o padrão para servidores de produção na Nuvem (AWS, Azure).

- Hipervisor Tipo 2 (Hosted) : Roda em cima de um Sistema Operacional hospedeiro (ex: VirtualBox, VMware, Workstation). Muito usado localmente por desenvolvedores.

Cada VM precisa de seu próprio Sistema Operacional Convidado (Guest OS) completo, o que significa que ela carrega drivers, bibliotecas, kernel e gerenciamento de memória próprios.

## 2. Virtualização em Nível de SO (Containerização)

É aqui que o DevOps brilha intesamente. Em vez de virtualizar o hardware para rodar vários sistemas operacionais, a containerização virtualiza o próprio sistema operacional para rodar aplicações isoladas.

Ferramentas como o Docker utilizam recursos nativos do Kernel do Linux (como Namespaces para isolamento de processos/rede e Cgroups para limitação de recursos de hardware) para criar ambientes isolados chamados Containers.

Os containers compartilham o mesmo Kernel do sistema hospedeiro. Eles contêm apenas a aplicação e suas dependências diretas (bibliotecas, variáveis de ambiente).

![[Pasted image 20260525173146.png]]![[Pasted image 20260525173216.png]]

![[Pasted image 20260525173340.png|286]]![[Pasted image 20260525173456.png]]