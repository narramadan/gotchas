# Quick reference to publish your static site to Surge

We can use `Surge` as a platform to deploy our static sites generated from node projects. Below are some quick references to get this done

`npm install -g surge` - Install Surge

As most of the static content generators build and put the content in `dist` or `public` folders, run the below command to get started and deploy the content to surge
`surge ./public/` 
  * Your email, password if you are not yet logged in.
  * Choose an appropriate domain to which the content should be uploaded and done
  * Content will be uploaded and pointed with the domain that is specified.
  * Access the url and you can see the content published and accessible

### Choose Domain to publish to when invoking
`surge ./public/ --domain XXXXXX.surge.sh` will use the domain that is provided by default

### Configure to not repeat asking Domain
`surge` will always prompt to enter domain when ever it is invoked. To not repeat this, add the below content in `CNAME` in folder under which index.html resides

`echo "XXXXXX.surge.sh" > CNAME` 

Now running `surge ./public/` from your project will not prompt domain for this project deployment
