# Rails API

### Learning Goals

* [ ] Return RESTful responses from a Rails backend
* [ ] Render JSON data from an endpoint
* [ ] Recognize situations where JSON APIs are appropriate
* [ ] Understand the HTTP request/response cycle


--------------------------

### Hook

1. Swap out json-server backend with Rails
    * show how to run rails as an API only backend
2. Rails can be run as just an API
3. CORS


### Lecture Flow

1. show how existing Rails app can serve JSON
2. spin up a new rails API app with postgres `rails new christmas-albums-api --api -G -d=postgresql`
    * talk about the difference with `--api` and `-d` flags
    * serves JSON instead of HTML
    * removes the view layer of Rails
3. create new resource for album `rails g resource Api::V1::Album title artist score:integer image`
4. show routes
5. fix migration, model
    * create and migrate db
    * create seed data
6. get index working in browser with serializer
    * talk about how serialization allows us to onfigure our JSON response
    * could use `gem fast_jsonapi`
7. CORS
    * uncomment `rack-cors` gem in Gemfile
    * change `app/config/initializers/cors.rb`
8. change api call in `index.js`


--
```ruby
def index
    @cows = Cow.all
        
    respond_to do |format|
      format.html { render :index }
      format.json { render json: @cows }
    end
end
``` 
--
```ruby
def index 
  albums = Album.all
  render json: albums
  # render json: albums, only: [:id, :title], include: :whatever
  # render json: AlbumSerializer.new(albums)
end
```
--
```ruby
# app/serializers/album_serializer.rb

class CandySerializer
  include FastJsonapi::ObjectSerializer
  attributes :name, :image, :likes, :id
  # has_many :customers
  # belongs_to :candy
end
```
--
```ruby
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```