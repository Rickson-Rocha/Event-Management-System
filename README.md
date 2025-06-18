
# Desafio Técnico - Desenvolvedor(a) Backend Jr - Event Management System



##  Sistema de Gestão de Eventos Culturais

Construir um sistema que permite a criação e gerenciamento de eventos culturais, controle de ingressos e participação de artistas.


## Regras de negócio
 As regras de negócio para construção desse desafio estão presentes no documento: [docs/regras_de_negocio.md](docs/)


### Entidades Principais

| Entidade      | Descrição |
|---------------|----------|
| **User**      | Usuário do sistema (com roles: PARTICIPANT, EVENT_CREATOR ou ADMIN) |
| **Event**     | Evento criado por um usuário |
| **Artist**    | Artistas participantes de eventos |
| **Location**  | Local onde o evento acontecerá |
| **Program**   | Programação detalhada de um evento |
| **Ticket**    | Ingresso adquirido por um participante |

---

## Perfis de Usuário e Permissões

| Role             | Permissões |
|------------------|-----------------------------|
| **PARTICIPANT**  | Consultar eventos públicos e comprar ingressos |
| **EVENT_CREATOR** | Criar, editar e excluir apenas os eventos que criou |
| **ADMIN**        | Visualizar todos os eventos de todos os criadores |

---



---

##  Mensageria (RabbitMQ)

- Ao comprar um ingresso, uma mensagem JSON deverá ser enviada para uma fila.



```json
{
  "participantId": 5,
  "eventId": 12,
  "ticketQuantity": 3,
  "purchaseTimestamp": "2025-06-18T14:00:00Z"
}
```


---

##  Requisitos Técnicos

- **Java 17+**
- **Spring Boot**
- **Spring Data JPA**
- **Spring Security + JWT**
- **RabbitMQ**
- **H2**
- **Docker / Docker Compose (para subir RabbitMQ)**
- **Testes / junit-mockito**

---


---

## ✅ Instruções para Rodar o Projeto Localmente

### Pré-requisitos

- Java 17+
- Docker + Docker Compose
- Maven

### Passo 1 - Subir o RabbitMQ ou Kafka com Docker

**Exemplo com RabbitMQ:**

```bash
docker run -d --hostname my-rabbit --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

RabbitMQ Management estará disponível em:  
[http://localhost:15672](http://localhost:15672)  
Login: guest / guest

---

### Passo 2 - Rodar a aplicação Spring Boot

```bash
./mvnw spring-boot:run
```


