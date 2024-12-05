# microservices-bookstore-argo-workflow 

>  This project contains a simple app based in four microservices containing infos about a book. The main goal of this repo was to practice and understand [Argo Workflows](https://argoproj.github.io/workflows/). 

<div align=>
	<img align="center" src=/.github/assets/img/argo.png>
</div> 


The services that the application consists are:

- productpage (Calls details and revies to populate the info page);
- details (Details about a book);
- reviews (Reviews about a book - Also calls ratings);
- ratings (Ratings about the book)

Databases:
- mongodb
- mysql

Simple diagram (Only calls, not cover databases)

![Diagram](/.github/assets/img/bookinfo.png)

You cand find the original repo [here](https://istio.io/v1.12/docs/examples/bookinfo/).
