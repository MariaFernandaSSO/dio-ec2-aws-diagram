# Primeiro Desafio de Projeto - Gerenciamento de Instâncias EC2 na AWS

Aprendemos a estruturar uma arquitetura de aplicação na AWS, compreendendo os papéis de cada serviço e como eles se conectam. (Usei como exemplo meu diagrama de sistema bancário.)

EC2: Instâncias configuradas para hospedar API e frontend, funcionando como ponto central de processamento, recebendo requisições do usuário e coordenando o acesso ao RDS e ao S3.
S3: Armazenamento de arquivos, como PDFs de extratos. A EC2 verifica se o arquivo já existe antes de acionar a Lambda, evitando processamento desnecessário.
Lambda Function: Automatiza tarefas, como gerar PDFs ou atualizar dados no banco, gravando resultados no S3 ou logs no RDS.
RDS: Banco de dados relacional com informações de contas, transações e saldos, acessado pela EC2 e pela Lambda.
Security Groups: Garantem boas práticas de segurança, controlando quem pode acessar a EC2 e outros recursos da rede.

Explicação enxuta:
O usuário faz uma requisição, que vai para a EC2 (API + frontend). A EC2 verifica se o PDF do extrato já existe no S3:
Se existir, retorna direto ao usuário.
Se não existir, chama a Lambda, que consulta o RDS, gera o PDF e salva no S3.
Depois, a EC2 retorna o PDF ou os dados ao usuário. O EBS pode ser usado na EC2 para armazenamento temporário ou logs, e os Security Groups garantem o acesso seguro à rede.
