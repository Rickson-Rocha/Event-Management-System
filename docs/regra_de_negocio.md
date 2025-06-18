
# 📏 Regras de Negócio - Event Management System

## 1. Capacidade Máxima de Participantes por Evento
- Cada evento deve possuir um campo `maxCapacity` (capacidade máxima de participantes).
- O sistema **não permitirá a venda de ingressos além desse limite**.
- Exemplo: Evento com capacidade de 100 pessoas → no máximo 100 ingressos vendidos.

---

## 2. Conflito de Local e Horário
- Não pode haver dois eventos marcados para o **mesmo local (`Location`) no mesmo dia e horário**.
- O sistema deve validar o conflito antes de criar um novo evento.
- Caso exista conflito, deve retornar erro informando que o local está indisponível.

---

## 3. Venda de Ingressos apenas para Eventos Futuros
- Um participante só pode comprar ingressos para eventos cuja **data de início ainda não ocorreu**.
- Eventos passados não podem ter venda de ingressos.

---

## 4. Restrições de Acesso para Criadores de Evento
- Usuários com perfil **`EVENT_CREATOR`** só podem **editar, excluir ou listar os eventos que eles próprios criaram**.
- Tentativas de manipular eventos de outros usuários devem resultar em erro de autorização.

---

## 5. Listagem de Eventos para Participantes
- Usuários com perfil **`PARTICIPANT`** podem **listar apenas eventos públicos (`PUBLIC`) com venda de ingressos ativa**.

---

## 6. Restrições de Alteração Após o Início do Evento
- Um evento só pode ser **editado enquanto ainda não tiver iniciado**.
- Após a data de início, qualquer tentativa de edição deve ser rejeitada.

---

## 7. Status de Evento
- Um evento pode assumir os seguintes status:
    - `DRAFT`: Rascunho, ainda não publicado.
    - `PUBLIC`: Publicado e com venda de ingressos liberada.
    - `CANCELLED`: Evento cancelado.
    - `FINISHED`: Evento encerrado (após a data de término).

- Apenas o **ADMIN** ou o **EVENT_CREATOR responsável** podem alterar o status do evento.

---

## 8. Limite de Ingressos por Participante
- Cada participante pode comprar **no máximo 5 ingressos por evento**.
- Caso ultrapasse esse limite, a compra deve ser recusada.

---

## 9. Obrigatoriedade de Artista para Publicação
- Um evento **não poderá sair de `DRAFT` para `PUBLIC` sem pelo menos um artista vinculado à sua programação**.

---

## 10. Mensageria na Compra de Ingressos
- Toda vez que um participante realizar uma compra de ingresso:
    1. O sistema deve persistir a compra no banco de dados.
    2. Em seguida, enviar uma mensagem JSON para a fila de mensageria.
    3. O consumidor (listener) apenas deverá imprimir a mensagem no console.

Exemplo de payload enviado:

```json
{
  "participantId": 5,
  "eventId": 12,
  "ticketQuantity": 3,
  "purchaseTimestamp": "2025-06-18T14:00:00Z"
}
```

---
