# Introduction

Activerecord.py provides ORM support to the existing [web.py](http://webpy.org/) python framework.

## Requirements

* Python 2.6+
* web.py 0.36+

## Installation

1. Install web.py using pip:

        $ pip install web.py

2. Download mvc.py:

        $ wget --no-check-certificate https://github.com/fedecarg/webpy-activerecord/archive/master.tar.gz
        $ tar xzvf master.tar.gz

3. Test Python examples:

        $ cd webpy-activerecord-master/src
        $ python activerecord.py

### Configuring a database

web.py works with many database systems, including MySQL, PostgreSQL and SQLite.

**SQLite**

```python
web.config.database = web.database(dbn='sqlite', db='db/example.sqlite')
```

**MySQL and Postgres**

If you choose to use MySQL or Postgres instead of the shipped SQLite database, your config/application.py will look something like this: 

```python
web.config.database = web.database(dbn='mysql', user='username', pw='password', db='example')
```

## Usage

### Rails ActiveRecord example

```ruby
class BooksController < ApplicationController

    def index
        @books = Book.find(:all)
    end
    
    def show
        @book = Book.find(params[:id])
    end
    
    def new
        @book = Book.new
        @subjects = Subject.find(:all)
    end
    
    def create
        @book = Book.new(params[:book])
        if @book.save
            redirect_to :action => 'index'
        else
            @subjects = Subject.find(:all)
            render :action => 'new'
        end
    end
    
    def delete
        Book.find(params[:id]).destroy
        redirect_to :action => 'index'
    end
end
```

### Web.py ActiveRecord example

```python
class BooksController(ApplicationController)

    def index(self):
        self.books = Book.find("all")
        
    def show(self, id):
        self.book = Book.find(id)
        
    def new(self):
        self.book = Book()
        self.subjects = Subject.find("all")
    
    def create(self):
        self.book = Book(self.input('book'))
        if self.book.save():
            self.redirect_to(action="index")
        else:
            self.subjects = Subject.find("all")
            self.render("new") 
    
    def delete(self, id):
        Book.find(id).delete()
        self.redirect_to(action='index')
```

## Feedback

If for whatever reason you spot something to fix but cannot patch it yourself, please open an issue.  Also, any kind of discussion regarding web frameworks is more than welcome @fedecarg



 
