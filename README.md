
# UAS Pemrosesan Data Tersebar

Aplikasi Pembelian dan Penjualan dengan menggunakan database Oracle, System Administrator menggunakan CodeIgniter dan Interface di Mobile Apps (Android). Komunikasi data antar Aplikasi menggunakan *RESTful Service* di oracle.


## Requirements

- [Virtual Box](https://www.virtualbox.org/wiki/Downloads) (Virtual Server)
- [Oracle Developer Day 11g](https://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html) (Database)
- [Android Studio](https://developer.android.com/studio) (Android IDE)
- [Codeigniter](https://www.codeigniter.com/) (Framework PHP)


## Tutorial

### Database

Aplikasi ini memiliki 5 table, yaitu :

1. [Customer](#table-customer)
2. [Barang](#table-barang)
3. [Penjualan](#table-penjualan)
4. [Pembelian](#table-pembelian)
5. [Supplier](#table-supplier)

#### Table Customer

![Table Customer!](./TableCustomer.PNG "Table Customer")

#### Table Barang

![Table Barang!](./TableBarang.PNG "Table Barang")

#### Table Penjualan

![Table Penjualan!](./TablePenjualan.PNG "Table Penjualan")

#### Table Pembelian

![Table Pembelian!](./TablePembelian.PNG "Table Pembelian")

#### Table Supplier

![Table Supplier!](./TableSupplier "Table Supplier")

### *RESTful Services*

![RESTful Services](./RestfulService.PNG)

PUT dan DELETE menggunakan {id} untuk mengidentifikasi data yang akan dieksekusi.  
Metode HTTP yang digunakan dalam aplikasi ini adalah:

| Method | Description |
| ------ | ------ |
| **GET** | ***menyediakan hanya akses baca pada _resource_*** |
| **POST** | ***digunakan untuk menciptakan _resource_ baru*** |
| **PUT** | ***digunakan untuk memperbarui _resource_ yang ada atau membuat _resource_ baru*** |
| **DELETE** | ***digunakan untuk menghapus _resource_*** |

*Resource Handler* & *Query* dapat dilihat pada gambar dibawah ini.

#### *RESTful Service* pada Barang

- **GET Barang**  
![GET](./GetBarang.PNG)

- **POST Barang**  
![POST](./PostBarang.PNG)
![POST Paramter](./Parameter.PNG)

- **PUT Barang**  
![PUT](./putbarang.PNG)
![PUT Paramter](./ParameterPut.PNG)

- **DELETE Barang**  
![DELETE](./DeleteBarang.PNG)


#### *RESTful Service* pada Customer

- **GET Customer**  
![GET](./restfulcustomer.PNG)

- **POST Customer**  
![POST](./postcustomerrestfull.PNG)
![POST Paramter](./postrestfullparameter.PNG)

- **PUT Customer**  
![PUT](./putcustomerrestfull.PNG)
![PUT Paramter](./parameterputrestfull.PNG)

- **DELETE Customer**  
![DELETE](./deleteputrestfull.PNG)

#### *RESTful Service* pada Penjualan

- **GET Penjualan**  
![GET](./getpenjualanrestfull.PNG)

- **POST Penjualan**  
![POST](./postpenjualanresstfull.PNG)
![POST Paramter](./postrestfullparameter.PNG)

#### *RESTful Service* pada Pembelian

- **GET Pembelian**  
![GET](./restfullgetpembelian.PNG)

- **POST Pembelian**  
![POST](./restfullpostpembelian.PNG)
![POST Paramter](./parameterpostrestfull2.PNG)

#### *RESTful Service* pada Supplier

- **GET Supplier**  
![GET](./restfullgetsupplier.PNG)

- **POST Supplier**  
![POST](./restfullpostsupplier.PNG)

- **PUT Supplier**  
![PUT](./restfullPutsupplier.PNG)

- **DELETE Supplier**  
![DELETE](./restfulldeletesupplier.PNG)

### *CodeIgniter*

[Script](./oracle-uas/application/libraries/Api.php) dibawah ini merupakan script php yang digunakan untuk mengakses *RESTful Services* dari Oracle menggunakan library [Goutte](https://github.com/FriendsOfPHP/Goutte).

```php
use GuzzleHttp\Client;

defined('BASEPATH') or exit('No direct script access allowed');

class Api
{
    private $client;

    public function __construct()
    {
        // base url yang digunakan untuk mengakses RESTful API
        $this->client = new Client(['base_uri' => 'http://192.168.43.75:8888/apex/obe/']);
    }

    public function request($method, $uri, $data = [])
    {
        // data di convert menjadi data JSON
        $options['json'] = $data;

        // jika metode HTTP nya adalah DELETE maka response yang diberikan adalah status code nya
        if ($method == 'delete') {
            $request = $this->client->request($method, $uri);
            return $request->getStatusCode();
        }

        $request = $this->client->request($method, $uri, $options);

        // response yang diberikan berupa content nya
        return $request->getBody()->getContents();
    }
}
```

#### Tampilan Web

- Barang
![List Barang](./barang.PNG)

- Customer
![List Customer](./customer.PNG)

- Penjualan
![List Penjualan](./penjualan.PNG)

- Pembelian
![List Pembelian](./pembelian.PNG)

- Supplier
![List Supplier](./supplier.PNG)

#### Tampilan Mobile Apps

![Gambar Android](./andro.PNG)
