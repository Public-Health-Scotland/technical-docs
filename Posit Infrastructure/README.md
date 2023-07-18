# Posit Infrastructure

[Posit Team](https://posit.co/products/enterprise/team/) enterprise applications have been deployed for [Public Health Scotland (PHS)](https://publichealthscotland.scot/) on the [Microsoft Azure](https://azure.microsoft.com/en-gb/) cloud computing platform.

The PHS deployment of Posit Team comprises three applications:

* [Posit Workbench](https://pwb.publichealthscotland.org/) - provides access to all the development environments RStudio, Jupyter and VS Code for both R and Python. Workbench has been designed to make use of the managed [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/products/kubernetes-service/#overview) to provide a scalable, performant and highly-available analytical environment. There is more information available about this in [Posit Workbench and Kubernetes](Posit%20Workbench%20and%20Kubernetes.md);
* [Posit Package Manager](https://ppm.publichealthscotland.org/) - a repository management server to organise and centralise R and Python packages across Public Health Scotland;
* Posit Connect - publish the things you create in both R & Python, including interactive applications, documents, notebooks, and dashboards. Deploy models as APIs, and configure reports to run on a custom schedule.
  
> Please note that the deployment of Posit Connect for PHS is still in development. See the [Posit Connect](https://posit.co/products/enterprise/connect/) website for more information in the meantime.

The infrastructure has been designed and implemented as a high-performance, high-availability analytical environment to support the work of Public Health Scotland. However, despite the computing power available, we need to be mindful at all times that this is a shared resource with finite capacity, and as such, we each have an individual responsibility to ensure our code is as optimised and efficient as possible, and that we use the Posit Team applications correctly and appropriately, to ensure what we all benefit from this resource equitably. Using inefficient code can cause your analysis to take longer or even cause the session to become unresponsive.
