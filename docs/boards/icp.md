# Kudos Boards for IBM Cloud Private
Basic instructions for deploying Kudos Boards into IBM Cloud Private for on-premise IBM Connections environments

### Pre-Requisites
1. IBM Spectrum CFC is installed and running
2. WebSphere environment with Web Server
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
4. Install helm (TODO add url)

### Login to kubectl
1. Open Spectrum Console
2. Go to `Admin` (top right)
3. Click `Config Client`
4. Copy the contents shown
5. Open your command line (cmd)
6. Paste the commands copied earlier and press enter


### Deploy Kudos Boards
1. Update helm values file
2. helm imstall command (TODO)
3. add new DNS record for Kudos Boards URL ie `boards.isw.net.au`

### Integrate into IBM Connections
Please follow [these instructions](/integration.md)

### Notes on IBM Spectrum CFC Naming
- Application (aka Deployments)
- PetSet (aka Replica sets)
