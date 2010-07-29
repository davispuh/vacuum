Sucker
======

Sucker is a thin Ruby wrapper to the [Amazon Product Advertising API](https://affiliate-program.amazon.co.uk/gp/advertising/api/detail/main.html). It runs on Curb and Crack and supports __everything__ in the API.

![Sucker](http://upload.wikimedia.org/wikipedia/en/7/71/Vacuum_cleaner_1910.JPG)

Examples
--------

Set up a worker.

    @worker = Sucker.new(
      :locale => "us",
      :key    => "API KEY",
      :secret => "API SECRET")

Fiddle with curl.

    @worker.curl { |c| c.interface = "eth1" }

Set up a request.

    @worker << {
      "Operation" => "ItemLookup",
      "IdType"    => "ASIN",
      "ItemId"    => ["0816614024", "0143105825"] }

Hit Amazon and do something with the response.

    pp @worker.get["ItemLookupResponse"]["Items"]["Item"]

Hit Amazon again.

    @worker << {
      "ItemId"  => ["0393329259", "0393317757"] }
    @worker.get

For some more examples, check the integration specs.

The unit specs should run out of the box, but the integration specs require you to create [an amazon.yml file with valid credentials](http://github.com/papercavalier/sucker/blob/master/spec/support/amazon.yml.example) in the spec/support folder. Of course, bundle install first.