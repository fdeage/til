# Using local Nokogiri with bundle: from 2 min to 15 sec

You need nokogiri (multiple parsing libraries: XML, HTML...) almost all the time in Ruby(Rails). But the library is big. Unless you use the system library to build it:

`env NOKOGIRI_USE_SYSTEM_LIBRARIES=true bundle install`

`time bundle install` gives
`60.58s user 30.55s system 84% cpu 1:47.90 total`

`time env NOKOGIRI_USE_SYSTEM_LIBRARIES=true bundle install` gives
`9.93s user 4.00s system 72% cpu 19.245 total`
