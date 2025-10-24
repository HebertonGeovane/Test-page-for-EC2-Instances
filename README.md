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
# Update the packages
sudo yum update -y

# Install Git and Apache
sudo yum install -y git httpd

# Starts and enables Apache
sudo systemctl start httpd
sudo systemctl enable httpd

# Clone the GitHub repository
cd /var/www/html
sudo git clone https://github.com/HebertonGeovane/Test-page-for-EC2-Instances.git

# Move the files to the Apache root directory
sudo cp -r Test-page-for-EC2-Instances/* /var/www/html/

# Adjust permissions
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
```

##  Autor
**Heberton Geovane**  
© 2025 - Projeto Educacional AWS  
🔗 [LinkedIn](https://www.linkedin.com/in/heberton-geovane/)
