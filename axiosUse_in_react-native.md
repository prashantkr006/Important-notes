##  Install axios
```
npm install axios
```
## Import axios in the component
```
import axios from 'axios'
```
## feetch data
 ### API url
```
const baseURL = "json_file_url"
```
### get request
```
const [product, setProduct] = useState(null);
  useEffect(() => {
    axios.get(`${baseURL}`).then((response) => {
      setProduct(response.data);
    });
  }, []);
```
### post request
```
const [product, setProduct] = useState(null);
  useEffect(() => {
    axios.get(`${baseURL}`).then((response) => {
      setProduct(response.data);
    });
  }, []);
```
### put request
```
  function updateProduct() {
    axios
      .put(`${baseURL}/1`, {
        title: "Hello World!",
        body: "This is an updated product."
      })
      .then((response) => {
        setProduct(response.data);
      });
  }
```
### Delete request
```
function deleteProduct() {
    axios
      .delete(`${baseURL}/1`)
      .then(() => {
        alert("Product deleted!");
        setProduct(null)
      });
  }
```

## How to Handle errors in axios
```
const [product, setProduct] = React.useState(null);
  const [error, setError] = React.useState(null);

  React.useEffect(() => {
    // invalid url will trigger an 404 error
    axios.get(`${baseURL}/asdf`).then((response) => {
      setProduct(response.data);
    }).catch(error => {
      setError(error);
    });
  }, []);
  
  if (error) return `Error: ${error.message}`;
  if (!post) return "No Product!"
```
* In this case, instead of executing the .then() callback, Axios will throw an error and run the .catch() callback function.

## Create an axios Instance
* it gets a bit tedious to keep writing that baseURL for every single request. Couldn't you just have Axios remember what baseURL you're using, since it always involves a similar endpoint?
* create an instance with the .create() method, Axios will remember that baseURL, plus other values you might want to specify for every request, including headers:
```
const client = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com/posts" 
});
```
* create and delete post
```
export default function App() {
  const [post, setPost] = React.useState(null);

  React.useEffect(() => {
    client.get("/1").then((response) => {
      setPost(response.data);
    });
  }, []);
  ```
  ```
  function deletePost() {
    client
      .delete("/1")
      .then(() => {
        alert("Post deleted!");
        setPost(null)
      });
  }
```
* The one property in the config object above is ```baseURL```, to which you pass the endpoint.</br>
The ```.create()``` function returns a newly created instance, which in this case is called client.
