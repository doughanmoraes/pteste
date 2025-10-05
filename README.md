# 🔒 Security Scanner Tool

![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-success)

Uma ferramenta automatizada de análise de segurança para websites que realiza testes abrangentes de vulnerabilidades, coleta informações de WHOIS, verifica cabeçalhos de segurança e identifica portas abertas.

## 📋 Índice

- [Recursos](#-recursos)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação](#-instalação)
- [Configuração](#-configuração)
- [Uso](#-uso)
- [Funcionalidades](#-funcionalidades)
- [Estrutura de Saída](#-estrutura-de-saída)
- [Vulnerabilidades Detectadas](#-vulnerabilidades-detectadas)
- [Avisos Legais](#-avisos-legais)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)

## 🚀 Recursos

- ✅ Verificação de disponibilidade de sites
- 🔍 Análise de cabeçalhos de segurança HTTP
- 🌐 Informações WHOIS detalhadas
- 🗺️ Geolocalização IP (GeoIP)
- 🔓 Scanner de portas com Nmap
- 🛡️ Análise de vulnerabilidades com Nikto
- 📊 Exportação de resultados em CSV
- 🎯 Análise automatizada de múltiplas URLs

## 📦 Pré-requisitos

### Software Necessário

- **Python 3.8+**
- **Nmap** - [Download](https://nmap.org/download.html)
- **Nikto** - Scanner de vulnerabilidades web
- **GeoLite2 Database** - Banco de dados de geolocalização

### Bibliotecas Python

```bash
requests
python-whois
python-nmap
geoip2
```

## 🔧 Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/security-scanner.git
cd security-scanner
```

### 2. Instale as dependências Python

```bash
pip install -r requirements.txt
```

**Arquivo `requirements.txt`:**
```
requests>=2.28.0
python-whois>=0.8.0
python-nmap>=0.7.1
geoip2>=4.6.0
```

### 3. Instale ferramentas externas

#### Windows
- **Nmap**: Baixe e instale de [nmap.org](https://nmap.org/download.html)
- **Nikto**: Requer Perl - [Instruções de instalação](https://github.com/sullo/nikto)

#### Linux (Debian/Ubuntu)
```bash
sudo apt-get update
sudo apt-get install nmap nikto
```

#### macOS
```bash
brew install nmap nikto
```

### 4. Configure o banco de dados GeoIP

1. Baixe o GeoLite2-City.mmdb de [MaxMind](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data)
2. Coloque o arquivo na raiz do projeto

## ⚙️ Configuração

### 1. Ajuste o caminho do Nmap

Edite a variável `nmap_path` na função `perform_nmap_scan()`:

```python
# Windows
nmap_path = r"C:\Program Files (x86)\Nmap\nmap.exe"

# Linux/macOS
nmap_path = "nmap"  # Geralmente já está no PATH
```

### 2. Crie o arquivo de URLs

Crie um arquivo `url.txt` na raiz do projeto com uma URL por linha:

```
https://example.com
https://testsite.org
https://mywebsite.com
```

## 🎯 Uso

### Execução Básica

```bash
python security_scanner.py
```

O script irá:
1. Ler todas as URLs do arquivo `url.txt`
2. Executar análises completas em cada site
3. Gerar um relatório CSV com os resultados

### Saída Esperada

```
Iniciando teste para: https://example.com
[Progresso da análise...]

Arquivo gerado: security_test_results.csv
```

## 🔍 Funcionalidades

### 1. **Verificação de Disponibilidade**
Testa se o site está online e acessível.

### 2. **Análise WHOIS**
Coleta informações sobre:
- Registrador do domínio
- Data de criação
- Data de expiração

### 3. **Cabeçalhos de Segurança**
Verifica a presença de:
- `Content-Security-Policy` (CSP)
- `X-XSS-Protection`
- `Strict-Transport-Security` (HSTS)
- `X-Frame-Options`

### 4. **Scanner de Portas (Nmap)**
- Executa scan SYN (`-sS`)
- Identifica portas abertas
- Lista serviços em execução

### 5. **Análise de Vulnerabilidades (Nikto)**
- Detecta vulnerabilidades conhecidas
- Identifica configurações inseguras
- Verifica versões desatualizadas de software

### 6. **Geolocalização IP**
- País e cidade do servidor
- Coordenadas (latitude/longitude)

## 📊 Estrutura de Saída

### Arquivo CSV

O arquivo `security_test_results.csv` contém as seguintes colunas:

| Coluna | Descrição |
|--------|-----------|
| URL | Endereço analisado |
| WHOIS | Informações de registro do domínio |
| GeoIP | Localização geográfica do servidor |
| Security Headers | Status dos cabeçalhos de segurança |
| Open Ports | Lista de portas abertas encontradas |
| Nikto Report | Relatório completo do Nikto |
| Vulnerabilities | Vulnerabilidades identificadas e classificadas |

## 🛡️ Vulnerabilidades Detectadas

### Classificação de Gravidade

| Vulnerabilidade | Gravidade | Impacto |
|-----------------|-----------|---------|
| CSP Ausente | 🔴 Alta | Permite ataques XSS |
| X-XSS-Protection Ausente | 🔴 Alta | Vulnerável a Cross-Site Scripting |
| HSTS Ausente | 🟡 Média | Possível downgrade de HTTPS |
| X-Frame-Options Ausente | 🟡 Média | Risco de Clickjacking |
| Portas Críticas Abertas | 🔴 Alta | Exposição de serviços sensíveis |

### Exemplo de Relatório de Vulnerabilidade

```python
{
    'Vulnerability': 'Content-Security-Policy (CSP) Ausente',
    'Gravidade': 'Alta',
    'Exploração': 'Injeção de código malicioso (XSS) pode ser feita em seu site.',
    'Solução': 'Implemente uma Política de Segurança de Conteúdo (CSP).'
}
```

## ⚠️ Avisos Legais

### 🚨 IMPORTANTE - USO ÉTICO

Esta ferramenta deve ser utilizada **EXCLUSIVAMENTE** para:
- Testes em sistemas que você possui ou tem autorização explícita
- Auditorias de segurança autorizadas
- Ambientes de teste e desenvolvimento próprios

### ⚖️ Responsabilidade

- O uso não autorizado desta ferramenta pode violar leis locais e internacionais
- O usuário é **totalmente responsável** pelo uso do software
- Os desenvolvedores não se responsabilizam por uso inadequado ou ilegal

### 📜 Conformidade Legal

Certifique-se de:
- ✅ Obter autorização por escrito antes de realizar testes
- ✅ Respeitar os termos de serviço dos sites testados
- ✅ Cumprir leis como LGPD, GDPR e Computer Fraud and Abuse Act

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 🐛 Reportando Bugs

Encontrou um bug? Abra uma [issue](https://github.com/seu-usuario/security-scanner/issues) com:
- Descrição detalhada do problema
- Passos para reproduzir
- Sistema operacional e versão do Python
- Logs de erro, se disponíveis

## 📝 Roadmap

- [ ] Interface gráfica (GUI)
- [ ] Suporte a proxies e VPN
- [ ] Relatórios em HTML/PDF
- [ ] Agendamento de scans automáticos
- [ ] Dashboard web para visualização de resultados
- [ ] Integração com APIs de threat intelligence

## 👥 Autores

- **Doughan Moraes** - *Desenvolvimento Inicial* - [GitHub](https://github.com/doughanmoraes)

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🙏 Agradecimentos

- Comunidade Nmap pelos excelentes scanners
- Projeto Nikto pela ferramenta de análise web
- MaxMind pelo GeoLite2 Database
- Comunidade open-source de segurança

## 📞 Suporte

- 📧 Email: contato@softpog.com.br


---

<div align="center">

**⭐ Se este projeto foi útil, considere dar uma estrela!**

Made with ❤️ for cybersecurity professionals

</div>
