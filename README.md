# CORS  

The CORS (Cross-Origin Resource Sharing) middleware in Lithe configures CORS headers to allow or restrict access to resources from different origins.  

---

## Installing the CORS Module

To use the CORS middleware in your Lithe project, you need to install the `lithemod/cors` package. Follow the steps below:

1. **Make sure you have Composer installed**. Composer is a dependency management tool for PHP.

2. **Open your terminal** and navigate to your Lithe project directory.

3. **Run the following command to install the module**:

   ```bash
   composer require lithemod/cors
   ```

   This will download and install the CORS module in your project, as well as automatically register any necessary dependencies.

## Using the CORS Middleware

The CORS middleware in Lithe is responsible for configuring Cross-Origin Resource Sharing headers, allowing or restricting access to your application's resources from different origins. To configure it in your application, add it using the `use()` method:

```php
use Lithe\Middleware\Configuration\cors;

$app->use(cors());
```

### Configuring the CORS Middleware

The CORS middleware can be configured with the following parameters:

- **origins**: Allowed origin(s) for accessing your resources. It can be a string or an array of strings. The default is `'*'` (any origin).
- **methods**: Allowed HTTP methods. The default is `'GET, POST, OPTIONS'`.
- **headers**: Allowed headers. It can be a string or an array of strings. The default is `'Origin, X-Requested-With, Content-Type, Accept'`.
- **credentials**: Indicates if credentials (such as cookies or authorization headers) are allowed. The default is `true`.
- **maxAge**: Time in seconds for caching the results of a preflight request. The default is `null`.

### Example Configuration:

```php
$app->use(cors([
    'origins' => ['https://example.com', 'https://another.com'],
    'methods' => 'GET, POST, PUT, DELETE, OPTIONS',
    'headers' => ['Content-Type', 'Authorization'],
    'credentials' => true,
    'maxAge' => 86400,
]));
```

### Middleware Behavior

- **Allowed Origins**: The middleware sets the `Access-Control-Allow-Origin` header with the allowed origins.
- **Allowed Methods**: Sets the `Access-Control-Allow-Methods` header with the permitted HTTP methods.
- **Allowed Headers**: Sets the `Access-Control-Allow-Headers` header with the allowed headers.
- **Credentials**: Sets the `Access-Control-Allow-Credentials` header to allow credentials if configured as `true`.
- **Cache Duration**: Sets the `Access-Control-Max-Age` header to specify the duration for caching preflight requests.
- **Handling OPTIONS Requests**: The middleware handles OPTIONS (preflight) requests by returning a 200 OK status and terminating the response.

## Considerations

- **Specific Origins**: If you specify concrete origins, only those origins will be able to access your resources.
- **HTTP Methods and Headers**: Configure the methods and headers according to your application's needs to ensure security and compatibility.
- **Preflight Requests**: The middleware ensures that OPTIONS requests are handled properly to support preflight requests.