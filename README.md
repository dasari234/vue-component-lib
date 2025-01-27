# Vue Component Library
### package Installation Guide
https://docs.github.com/en/packages/quickstart
   <ul>
      <li>Step 1: Create Your Repository (First, create a new repository on GitHub for your package)</li>
      <li>Step2: Prepare Your Package (Clone your repository to your local machine)</li>
      <li>Step3: (Add the GitHub repository to your package.json) {
  "repository": {
    "type": "git",
    "url": "https://github.com/your-username/your-repo-name.git"
  }
}</li>
<li>Add a .npmrc file to the root of your project to configure npm to use GitHub Packages: (echo "//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}" > .npmrc)</li>
      <li>Create a GitHub personal access token (PAT) with the write:packages scope, GitHub Settings > Developer settings > Personal access tokens > Generate new token</li>
      
      <li>To install the Comman UI library, run the following command: npm install @vigo-mvm/vigo-vue-component-lib@0.0.9</li>
   </ul>
    
### styles
    import "../node_modules/@dasari234/vue-component-lib/dist/style.css"; in to main.ts
### 1. Title Component
   **Props** <br/>
     <ul>
        <li>size = { type: Number, default: 12 } </li>
        <li>color = { type: String, default: "#000000" }</li>
        <li>title = { type: String, default: "Sample Text" } </li>
     </ul>

### 2. CopyClipboard Component
   **Props** <br/>
     <ul>
        <li>text = { type: String, default: "Sample Text" } </li>
     </ul>