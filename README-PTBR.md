# Edge Toolkit

```text
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⠄⠀⠀⠀⢀⣴
⠀⠀⠀⠀⠀⠀⠀⢀⣠⣤⣤⣙⠋⠀⠀⢀⣴⣿⡇⠀⠀⠀⠀⠀⡰
⠀⠀⢀⣠⣤⣶⢿⣏⢉⠉⠒⠂⠀⠠⣀⠛⠿⡼⠀⠀⠀⠀⢀⡔⠁
⣰⣇⣸⣯⣷⣾⣿⣿⣾⠇⢀⣀⣠⣮⣮⢧⢰⠀⠀⠀⢀⣴⡟⠀⠀⡀
⢻⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⡿⣱⠏⠀⣀⣴⣾⣿⣷⣤⣾⠁
⣇⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⡱⢃⣠⣾⣿⣿⣿⢿⣿⣿⢃⡄
⣭⡛⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣾⣾⣿⣿⣿⣿⣿⣿⣼⣿⣧⡟
⣿⣿⣷⣮⣙⠿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠿⠿⣿⢇⣿⠟⠄⣼
⢿⣿⣿⣿⣿⣷⣮⡝⣿⣿⢟⣉⣙⡫⠭⠭⠛⠛⣛⣿⣶⡿⣩⡾⣸⣿
⠘⣿⣿⣿⣿⣿⠟⣵⡿⢡⣿⣿⣿⣿⢸⢀⣠⣾⣿⠿⠋⣼⣿⢣⣿⣿
⠀⣿⣿⣿⡿⢃⠻⣿⣧⣂⠭⠭⠭⠕⣢⣾⡿⡋⣴⣾⢸⡟⠟⣼⣿⣿
⠀⢻⡿⢟⣴⣿⣿⣮⡙⠿⣿⣿⣿⡿⢛⣵⣾⣇⢿⡿⡜⢧⠀⣿⣿⠿
⠀⠘⣱⣾⣿⣿⣿⣿⣿⣷⣦⣭⣵⣾⣿⠿⠿⣛⡼⣼⡿⡷⣭⡭⣵⣿
```

Para minhas aplicações Next.js, normalmente utilizo PostgreSQL, Nginx, Cloudflare Origin Certificates, Node.js e PM2. Configurar e instalar manualmente todos esses componentes é um processo trabalhoso e sujeito a erros. Por isso, criei este toolkit para automatizar a instalação e a configuração da infraestrutura necessária para implantar e executar aplicações Next.js.

Basta clonar o repositório, executar o comando `edge` e o ambiente estará pronto para uso. O toolkit também inclui um MOTD personalizado e um comando dedicado para acessar o menu de gerenciamento das ferramentas instaladas.

Sinta-se à vontade para estender o toolkit, adicionar novos recursos ou contribuir com melhorias. O objetivo é evoluí-lo para um toolkit de provisionamento de servidores mais poderoso e flexível ao longo do tempo, oferecendo suporte a ferramentas, serviços e cenários de implantação adicionais. Contribuições e novas ideias são bem-vindas. Quanto mais recursos adicionarmos, mais útil ele se tornará para provisionar rapidamente ambientes prontos para produção.

## Instalação

Clone o repositório e navegue até o diretório do projeto:

```bash
git clone https://github.com/0x66616C6C656E/edgekit.git
cd edgekit
```

O repositório contém dois arquivos principais:

* `edge` — código-fonte da CLI `edge`, instalada em `/usr/local/bin/edge`.
* `motd` — MOTD (Message of the Day) personalizado exibido quando os usuários fazem login via SSH.

### 1. Instalar a CLI `edge`

Instale o comando `edge` em todo o sistema e torne-o executável:

```bash
sudo cp edge /usr/local/bin/edge
sudo chmod +x /usr/local/bin/edge
```

Você pode verificar a instalação com:

```bash
edge --help
```

### 2. Configurar o MOTD

Em sistemas baseados em Debian, como o Ubuntu, o Message of the Day pode ser gerado dinamicamente por scripts localizados em `/etc/update-motd.d/`. Esses scripts podem adicionar ou substituir o conteúdo exibido durante o login via SSH.

Para garantir que o MOTD do Edge Toolkit seja exibido de forma consistente, desative os scripts padrão do MOTD:

```bash
sudo chmod -x /etc/update-motd.d/*
```

Em seguida, instale o MOTD personalizado:

```bash
sudo cp motd /etc/motd
```

Verifique o MOTD instalado:

```bash
cat /etc/motd
```

Você também pode executar manualmente os scripts do MOTD para testar a configuração dinâmica do sistema:

```bash
sudo run-parts /etc/update-motd.d/
```

Por fim, abra uma nova sessão SSH para verificar se o MOTD personalizado está sendo exibido corretamente durante o login.

> **Observação:** Desativar os scripts não os remove do sistema. Isso apenas impede que sejam executados. Eles podem ser reativados a qualquer momento com `chmod +x`.

### 3. Iniciar o Toolkit

Depois que a CLI `edge` estiver instalada, inicie a interface de gerenciamento:

```bash
sudo edge
```

O comando `edge` fornece acesso ao menu de gerenciamento do toolkit e às operações de infraestrutura disponíveis.

### 4. Instalar a Stack Necessária

No toolkit, utilize o comando de instalação para provisionar a infraestrutura necessária:

```bash
sudo edge --install
```

Isso instala e configura os principais componentes necessários para um ambiente típico de produção com Next.js, incluindo:

* Node.js
* PM2
* Nginx
* PostgreSQL
* Cloudflare Origin Certificates

Após a conclusão do processo de instalação, o servidor estará pronto para a implantação de aplicações Next.js.

## Fluxo de Instalação Manual

Para uma configuração rápida, todo o processo de instalação pode ser realizado com:

```bash
git clone https://github.com/0x66616C6C656E/edgekit.git
cd edgekit

sudo cp edge /usr/local/bin/edge
sudo chmod +x /usr/local/bin/edge

sudo chmod -x /etc/update-motd.d/*
sudo cp motd /etc/motd

sudo edge --install
```

Depois da instalação, utilize:

```bash
sudo edge
```

para acessar a interface de gerenciamento do Edge Toolkit.
