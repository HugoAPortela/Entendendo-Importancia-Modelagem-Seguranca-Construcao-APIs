### Códigos de Retorno

As requisições processadas por nossa API retornarão códigos de resposta em HTTP, sendo as mais relevantes as descritas a seguir:

| Código HTTP | Descrição                                                    |
| :---------- | :----------------------------------------------------------- |
| 200         | Indica que o processamento foi realizado corretamente e o retorno será conforme a expectativa. |
| 201         | Indica que o recurso foi processado com sucesso e terá a confirmação e/ou identificação do novo registro na resposta da requisição. |
| 400         | Requisição mal formatada.                                    |
| 401         | Requisição requer autenticação. Acontece quando não é enviado o Access Token na requisição ou é utilizando um que está inválido. |
| 403         | Requisição negada.                                           |
| 404         | Recurso não encontrado.                                      |
| 5xx         | Erro interno inesperado do servidor.                         |