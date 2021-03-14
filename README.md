# SqlGen
**This software is written for the article. [link](https://medium.com/@changhengliou/%E7%94%A8mysql-fulltext-search%E5%BB%BA%E7%AB%8B%E7%B0%A1%E6%98%93%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E-80659c28ec19)**

## To use this, please first execute the following sql.

```
--MySQL
CREATE DATABASE wikidump;
USE wikidump;
CREATE TABLE IF NOT EXISTS PagesArticles (
  `id`    int not null auto_increment,
  `url`   varchar(255),
  `title` varchar(255),
  `text`  mediumtext,
  FULLTEXT `fulltext_index` (`title`, `text`),
  primary key (`id`)
) ENGINE = InnoDB CHARACTER SET = utf8mb4;

--SQL Server
CREATE TABLE [dbo].[PagesArticles](
	[id] [int] IDENTITY(1,1) NOT NULL,
	[url] [varchar](255) NULL,
	[title] [varchar](255) NULL,
	[text] [text] NULL,
PRIMARY KEY CLUSTERED 
(
	[id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO

```

## Import Database Connection Driver
go get github.com/go-sql-driver/mysql
go get github.com/denisenkom/go-mssqldb

## Build
go build sqlgen.go

## Usage
`./sqlgen -dbms [MYSQL/MSSQL] -dbip [DBIP] -dbport [port] -dbuser [DBUSER] -dbpwd [password]  -dbname [DBName] -tablename [DBTable] -textpath [wiki_file_dir]`

**Example(MySQL、Linux Path)**

`./sqlgen -dbms MYSQL -dbip 127.0.0.1 -dbport 3306 -dbuser sqluser -dbpwd sqlpassword -dbname wikidump -tablename PagesArticles -textpath /wikidump/rawdata/text`

**Example(SQL Server、Windows Path)**

`./sqlgen -dbms MSSQL -dbip 127.0.0.1 -dbport 1433 -dbuser sqluser -dbpwd sqlpassword -dbname wikidump -tablename PagesArticles -textpath D:\wikidump\text`
