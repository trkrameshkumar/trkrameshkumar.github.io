This is part 2 of a 2-part tutorial series.

In this part two of this tutorial we will going to tech you have to enable Datatables with ajax functionality to our html table.

To enable datatables we have to two things

1. Generate custom datatable configuration file

1. Configure custom datatable configuration file for your model

1. Initialize datatables on the following files 

(for this example we are going to work on user related files witch we already created on previous part of this tutorial)

  *  app/views/users/index.html.erb
  *  app/controllers/users_controller.rb
  *  app/assets/javascripts/users.js.coffee


### Generate custom datatable configuration file

```
rails generate datatable User
```

This will generate a file named `user_datatable.rb` in `app/datatables`. 

### Configure custom datatable configuration file for your model(my case the file is user_datatable.rb)

**Before making any change the file will look like this**

```
# uncomment the appropriate paginator module,
# depending on gems available in your project.
# include AjaxDatatablesRails::Extensions::Kaminari
# include AjaxDatatablesRails::Extensions::WillPaginate
# include AjaxDatatablesRails::Extensions::SimplePaginator

def sortable_columns
  # list columns inside the Array in string dot notation.
  # Example: 'users.name'
  @sortable_columns ||= []
end

def searchable_columns
  # list columns inside the Array in string dot notation.
  # Example: 'users.name'
  @searchable_columns ||= []
end
```

* For `paginator options`, just uncomment the paginator you would like to use, given the gems bundled in your project. For example, if your models are using `Kaminari`, uncomment `AjaxDatatablesRails::Extensions::Kaminari`. 

* For sortable_columns, assign an array of the database columns that correspond to the columns in our view table. For `example [users.name, users.phone]`. This array is used for sorting by various columns.

* For searchable_columns, assign an array of the database columns that you want searchable by datatables. For `example [users.name, users.phone]`

* For listing record from database to table you have to select what are all the attributes you are going to list on the html table on the `data` funciton.

```
def data
end 
```

* For selecting query you have to define in this function

```
get_raw_records
```

**For this example project i have these requirements**

> I need searchable on these two attributes

1. name
1. phone 

> And i need sortable columns for these two 

1. name
1. phone

> And i would like to print the following attributes on the table

1. name
1. phone
1. address

> And i am using kaminari for pagination



**After making changes my UserDatatable.rb file will look like this**

```
class UserDatatable < AjaxDatatablesRails::Base
  # uncomment the appropriate paginator module,
  # depending on gems available in your project.
  include AjaxDatatablesRails::Extensions::Kaminari
  # include AjaxDatatablesRails::Extensions::WillPaginate
  # include AjaxDatatablesRails::Extensions::SimplePaginator

  def sortable_columns
    # list columns inside the Array in string dot notation.
    # Example: 'users.name'
    @sortable_columns ||= ['users.name' ,'users.phone']
  end

  def searchable_columns
    # list columns inside the Array in string dot notation.
    # Example: 'users.name'
    @searchable_columns ||= ['users.name' ,'users.phone']
  end

  private

  def data
    records.map do |record|
      [
        record.name,
        record.phone,
        record.address
      ]
    end
  end

  def get_raw_records
    User.all
  end

end
```

### Initialize datatables on the following files

  *  app/views/users/index.html.erb
  *  app/controllers/users_controller.rb
  *  app/assets/javascripts/users.js.coffee

**Initialize on view file (app/views/users/index.html.erb)**

```
<table id="users-table", data-source="<%= users_path(format: :json) %>">
  <thead>
    <tr>
      <th>Name</th>
      <th>Phone</th>
      <th>Address</th>
      <th colspan="3"></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
```

**Initialize on controller index action on this file (app/controllers/users_controller.rb)**

```
  def index
    respond_to do |format|
      format.html
      format.json { render json: UserDatatable.new(view_context) }
    end
  end
```

**Initialize js on this file (app/assets/javascripts/users.js.coffee)**

```
$ ->
  $('#users-table').dataTable
    processing: true
    serverSide: true
    ajax: $('#users-table').data('source')
    pagingType: 'full_numbers'
```
**Congratulations** Now when you visit the app in your browser, at http://localhost:3000, you should see this:

![image from imgur](http://i.imgur.com/OpwQW3Z.png)


You have successfully integrated and enabled datatables on your project . Thank you for reading .