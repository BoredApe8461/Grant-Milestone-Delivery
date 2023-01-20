# Milestone Delivery :mailbox:



**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/milestone-deliverables-guidelines.md).**  


* **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/ink-smart-contract-wizard.md

* **Milestone Number:**  2

* **Code repository:**

 - https://github.com/avirajkhare00/ink-wizard
 - https://github.com/avirajkhare00/homebrew-ink-wizard
 - PyPi: https://pypi.org/project/ink-wizard/


**Deliverables**


### Milestone - 2

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | Apache License 2.0 | All code will be published under Apache 2.0 https://github.com/avirajkhare00/ink-wizard/blob/main/LICENSE https://github.com/avirajkhare00/homebrew-ink-wizard/blob/main/LICENSE |
| 0b. | Documentation | We will provide both inline documentation of the code and a basic tutorial that explains how a user can run the CLI to generate the smart contracts. https://github.com/avirajkhare00/ink-wizard/blob/main/README.md https://github.com/avirajkhare00/homebrew-ink-wizard/blob/main/README.md |
| 0c. | Testing and it's Guide | Core functions will be fully covered by comprehensive unit tests written using unittest package to ensure functionality and robustness. In the guide, we will describe how to run these tests. https://github.com/avirajkhare00/ink-wizard/tree/main/tests/commands |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. https://github.com/avirajkhare00/ink-wizard/blob/main/Dockerfile |
| 0e. | Articles | We will publish an article on Medium on how to use this CLI tool. |
| 0. | Smart Contract Generator CLI | We will be building this CLI using Typer package using which we can create interactive CLI. https://github.com/avirajkhare00/ink-wizard/tree/main/ink_wizard/commands |
| 1. | Push the Python package to PyPi | We will push this python package to PyPi so that users can install the package using pip3. https://pypi.org/project/ink-wizard/ |
| 2. | Creation of formula for CLI | We will be creating homebrew formula so that users can easily install this CLI tool. Since most of the substrate ecosystem users use Rust, having formula will remove dependency to install python. https://github.com/avirajkhare00/homebrew-ink-wizard/blob/main/Formula/ink-wizard.rb |
