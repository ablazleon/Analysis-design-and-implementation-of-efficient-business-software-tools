# Retos a los que me enfrenté

A parte del reto de intentar hacer un producto SaaS, destaco varias tareas paralelas>

1- How to publish the summaries that I am creating how to make them accesible

word => pdf (depend on an office 365 licencse?) 70€/year
markdown => difficult to update citations
https://www.freecodecamp.org/news/taking-off-the-successful-launch-of-an-open-source-book-7553a2262898/
https://leanpub.medium.com/why-dont-i-use-leanpub-4ad2a77f5744
https://geocompr.github.io/user_19/presentation/#18
blog (like medium) => easier to be found difficult to update citations
latex (with overleaf) => general thing I have to present. HO w to facilitate reviews => althoug github and markwond is cool
PS: not with meister mind beacuse colalboartion is only allowed in paid plan

Why I want it to be public? => beacuse i Want people to share their experiences. I share some state based on effort, and otehr people can:
- mantain the state so is easier to justify the decision: let's take some more effort and deploy it yourself. In which way? In the way that it is useful?
- => I submitted it, but this rasteator idea of how to support teh digital transofmraotin of a business, I dont want to be fixed it can continue
-  ¿Cómo web apra comparar algo apra ver cuál es el mejor?
-  No, tiene que ser en plan orgnaización: en cualuqier momento se puede hacer un fork, los que ocntribuyen. Awsoeme
- Overleaf, pq word está bien, vetnajas pero el ivnocnenivente de para mantener esa lsita online es difícil
- cómo es la coalboración en latex? Se me va de las manos con overleaf. En word voy aescribiendo eso y se lo voy mandando
- lo bueno ahora de owrd, es que en rela time pod´ria verlo
- en latex también: con comentarios, versión de una cosas versión de otra
- con word autoría, tiempo real y concocimiento previo vs mejor formato

2- Sql vs Nosql for eccomerce with Saleor

https://medium.com/@ablazleon/nosql-vs-sql-para-ecommerce-con-saleor-707bc5851407

3- Design thinking> entender c'omo apclairlo
https://www.salesforce.com/uk/blog/2017/10/design-thinking-questions-to-help-you-embrace-innovation.html

4- Anexo problema 1 iam y actualizacion del cli de aws a 2

Problema con iam:

https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html

couse: AWS OTP-AWSD7
AWS: Getting Started with Cloud Security

Con copilot un multi az

https://aws.amazon.com/blogs/containers/introducing-aws-copilot/
Cost of the stack: https://stackoverflow.com/questions/65337280/how-to-get-budget-estimate-for-copilot

https://community.bitnami.com/t/help-on-architecture-for-odoo-deployment-with-multiple-sites-1-db/93346

with steps: https://aws.amazon.com/blogs/compute/building-deploying-and-operating-containerized-applications-with-aws-fargate/

with cli: https://aws.amazon.com/blogs/containers/running-wordpress-amazon-ecs-fargate-ecs/

Temproary managed credneitals
```
✘ execute "env upgrade --app demo --name test": get template version of environment test in app demo: get metadata for stack demo-test: get template summary: InvalidClientTokenId: The security token included in the request is invalid
        status code: 403, request id: f2dd98e8-f84c-4ef0-acc5-2a78d7c2aab5
        
        
admin:~/environment/demo-app (master) $ aws sts get-session-token --serial-number arn:aws:iam::764217278004:mfa/admin --token-code 273414

An error occurred (InvalidClientTokenId) when calling the GetSessionToken operation: The security token included in the request is invalid        
```

```
sudo curl -Lo /usr/local/bin/copilot https://github.com/aws/copilot-cli/releases/latest/download/copilot-linux \
   && sudo chmod +x /usr/local/bin/copilot \
   && copilot --help
```

no puedo isntalar docker en cloud shell y en cloud9 da problemas de iam.

aws cli 2 for copilot init

Then the wordpress https://github.com/bvtujo/copilot-wordpress

It seems it needs aws cofnigure after disabling it, it continue not working
