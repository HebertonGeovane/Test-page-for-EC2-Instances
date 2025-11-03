#  AWS EC2 Test Page

Este projeto é uma **página de teste para instâncias Amazon EC2**.

---

## 🚀 Sobre o Projeto
Esta página demonstra:
- Como detectar automaticamente a **Região** e a **Zona de Disponibilidade** (AZ) de uma instância EC2;
- Uma **interface moderna** feita com **Tailwind CSS e AOS**;
- Um **rodapé com créditos e LinkedIn** do criador.

---

##  Tecnologias Usadas
- HTML5  
- Tailwind CSS  
- AOS (Animate On Scroll)  
- Phosphor Icons  
- JavaScript  
- AWS EC2 Metadata API (IMDSv2)

---

## 🖥️ Execução Local
1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` em um navegador.
3. (Opcional) Se estiver em uma instância **EC2**, a página exibirá automaticamente a **Região e AZ**.

---
User Data - Deploy Automático da Página

 Esse script faz o deploy automático do seu site quando a instância EC2 é iniciada.
Ele instala o Apache, clona o repositório e exibe a página diretamente no navegador via IP público da instância.

```
#!/bin/bash
# Update packages
sudo yum update -y

# Install Git and Apache
sudo yum install -y git httpd

# Start and enable Apache
sudo systemctl start httpd
sudo systemctl enable httpd

# Clone the repository
cd /var/www/html
sudo git clone https://github.com/HebertonGeovane/Test-page-for-EC2-Instances.git
sudo cp -r Test-page-for-EC2-Instances/* /var/www/html/

# ===== Get IMDSv2 token =====
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600" -s)

# ===== Fetch metadata =====
AZ=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
-s http://169.254.169.254/latest/meta-data/placement/availability-zone)
REGION=${AZ::-1}

# ===== Insert into the page =====
sudo sed -i "s/<span id=\"region\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"region\" class=\"font-semibold text-cyan-300\">${REGION}<\/span>/g" /var/www/html/index.html

sudo sed -i "s/<span id=\"az\" class=\"font-semibold text-cyan-300\">Detecting...<\/span>/<span id=\"az\" class=\"font-semibold text-cyan-300\">${AZ}<\/span>/g" /var/www/html/index.html

# Permissions
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
```

##  Autor
**Heberton Geovane**  
© 2025 - Projeto Educacional AWS  
🔗 [LinkedIn](https://www.linkedin.com/in/heberton-geovane/)
