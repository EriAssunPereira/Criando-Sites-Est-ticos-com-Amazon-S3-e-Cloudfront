# Criando-Sites-Estáticos-com-Amazon-S3-e-Cloudfront

### Criando Sites Estáticos com Amazon S3 e CloudFront

Neste tutorial, vamos explorar como utilizar os serviços da AWS, Amazon S3 e CloudFront, para criar e publicar sites estáticos de maneira eficiente e escalável.

#### **1. Introdução**

Atualmente, a hospedagem de sites estáticos é uma prática comum, especialmente para aplicações que não requerem processamento no servidor. Utilizando Amazon S3 (Simple Storage Service) e CloudFront, podemos criar uma solução robusta que combina armazenamento de objetos com distribuição de conteúdo global via CDN (Content Delivery Network).

#### **2. Benefícios de utilizar Amazon S3 e CloudFront**

- **Amazon S3**: Oferece armazenamento seguro e altamente escalável para conteúdo estático, como HTML, CSS, JavaScript, imagens e arquivos de mídia.
  
- **CloudFront**: CDN que distribui o conteúdo globalmente, melhorando a velocidade de entrega ao usuário final através da colocação do conteúdo mais próximo geograficamente.

#### **3. Configuração do Ambiente**

Antes de começar, certifique-se de ter uma conta na AWS e configurar suas credenciais no ambiente local. Vamos dividir nosso projeto em módulos para facilitar a compreensão e organização do código.

##### **Módulo 1: Configuração do Amazon S3**

1. **Criar um Bucket no Amazon S3**:
   
   Primeiro, precisamos criar um bucket no Amazon S3 para armazenar os arquivos do nosso site estático. Aqui está um exemplo de código usando a AWS CLI (Command Line Interface):
   
   ```bash
   aws s3 mb s3://meu-site-estatico
   ```

2. **Configurar Políticas de Bucket**:
   
   Para permitir acesso público aos arquivos no bucket, criaremos uma política de bucket. Substitua `<seu-bucket>` pelo nome do seu bucket.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::<seu-bucket>/*"
           }
       ]
   }
   ```

##### **Módulo 2: Upload de Arquivos**

1. **Upload de Arquivos para o Amazon S3**:
   
   Após configurar o bucket, podemos enviar os arquivos estáticos para ele. Use o comando abaixo para copiar arquivos locais para o S3:

   ```bash
   aws s3 cp /caminho/local/para/seu/site s3://meu-site-estatico --recursive
   ```

##### **Módulo 3: Configuração do CloudFront**

1. **Criar uma Distribuição do CloudFront**:
   
   Agora, configuraremos o CloudFront para distribuir nosso site estático globalmente:

   - Vá para o Console da AWS e navegue até CloudFront.
   - Clique em "Create Distribution" e selecione "Get Started" sob "Web".
   - Configure as origens, opções de cache e demais configurações conforme necessário.

2. **Ajustar as Configurações de Origem**:
   
   Defina a origem como o bucket S3 criado anteriormente. Isso garante que o CloudFront distribua o conteúdo corretamente.

3. **Configurar DNS**:
   
   Configure seu DNS para apontar para o domínio fornecido pelo CloudFront para garantir que seu site seja acessível pelo domínio personalizado.

#### **Conclusão**

Ao seguir este guia, podemos configurar com sucesso uma solução para hospedar um site estático utilizando Amazon S3 para armazenamento e CloudFront para distribuição global de conteúdo. Essa abordagem não apenas é escalável e eficiente, mas também melhora significativamente a performance e a segurança do seu site estático.

