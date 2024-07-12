# Ruby on Rails microblog application

This is an application which was made during reading "Ruby on Rails tutorial" book.

## License

All source code in the [Ruby on Rails Tutorial] (https://www.railstutorial.org/)
is available jointly under the MIT License and the Beerware
License. See [LICENSE.md](LICENSE.md) for details.

### Getting started

To get started with the application you should clone the repository and then install required gems:
```
gem install bundler -v 2.3.14
bundle _2.3.14_ config set --local without 'production'
bundle _2.3.14_ install
```

Next you should migrate the database:
```
rails db:migrate
```

Then you should run the tests to make sure that everything is OK:
```
rails test
```

If the test suite passes, the app is ready for running on a local server:
```
rails server
```

Link to *the book*
(https://www.railstutorial.org/book).
