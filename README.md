# apache2_https_ubuntu

## 📖 Descrição

Role Ansible para instalação e configuração de SSL no Apache2 utilizando certificados gerados localmente com **[mkcert](https://github.com/FiloSottile/mkcert)**.

Essa role realiza:

- Instalação do `mkcert` na versão desejada
- Criação da autoridade certificadora local (CA)
- Geração de certificados para os domínios informados
- Configuração de VirtualHost HTTPS no Apache2 com SSL
- Ativação do módulo SSL e site configurado

> 📌 **Compatível e testado em Ubuntu.** Pode funcionar em Debian, mas **não foi testado oficialmente**.

---

## 📑 Requisitos

- Ansible 2.12+
- Sistema operacional baseado em Ubuntu (testado no Ubuntu 22.04)
- Apache2 instalado previamente no servidor-alvo

---

## 📦 Variáveis

Você pode configurar as seguintes variáveis em `defaults/main.yml`:

| Variável         | Descrição                                    | Valor padrão               |
|:----------------|:---------------------------------------------|:---------------------------|
| `mkcert_version` | Versão do mkcert a ser instalada             | `"1.4.4"`                   |
| `cert_path`      | Caminho para armazenamento dos certificados  | `"/etc/ssl/certs"`          |
| `key_path`       | Caminho para armazenamento das chaves privadas | `"/etc/ssl/private"`       |
| `mkcert_bin_path`| Caminho do binário mkcert no servidor         | `"/usr/local/bin/mkcert"`   |
| `domain_name`    | Nome do domínio principal                    | `"noto.local"`              |
| `server_name`    | Valor do `ServerName` no VirtualHost do Apache | `"zabbix.noto.local"`       |

---

## 📂 Estrutura da Role

```
apache2_https_ubuntu/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
├── tests/
├── vars/
└── README.md
```

---

## 📋 Uso

### 📌 Exemplo de Playbook

```yaml
- name: Configurar HTTPS no Apache com mkcert
  hosts: all
  become: yes
  roles:
    - role: apache2_https_ubuntu
```

### 📌 Teste Local

Em `tests/test.yml`:

```yaml
- name: Testa aplicação da role
  hosts: localhost
  gather_facts: false
  tasks:
    - name: Dummy task
      ansible.builtin.debug:
        msg: "Testando role"
```

---

## 📎 Dependências

Nenhuma.

---

## ⚠️ Observações

- Esta role **foi testada apenas em Ubuntu**.  
- Pode funcionar em **Debian**, mas **não há garantia de funcionamento sem testes prévios**.
- O Apache2 deve estar previamente instalado no servidor-alvo.

---

## 📚 Referências

- [Mkcert — GitHub](https://github.com/FiloSottile/mkcert)
- [Ansible Documentation](https://docs.ansible.com/)
- [Apache SSL Configuration](https://httpd.apache.org/docs/current/ssl/ssl_howto.html)

---

## 📄 Licença

MIT

---

## 🤝 Autor

Desenvolvido por **josezipf**
https://nototi.com.br
