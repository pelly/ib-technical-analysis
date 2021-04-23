# ib-technical-analysis
A library for performing technical analysis

This Gem is inspired by the [intrinio package](https://github.com/intrinio/technical-analysis).

It fits perfect into the **_IB-Ruby_** suite, but can be used isolated, too.

### Perform calculation on time-series


`IB-Technical-Analysis` calculations are embedded in the `Enumerator`-class.

Thus
```ruby
require 'bundler/setup'
require 'ib-gateway'
require 'ib/eod'
require 'ib/symbols'
require 'technical-analysis'

using TASupport

z = Symbols::Futures.mini_dax.eod( duration: '50 d').each
zz= z.calculate( :ema, period: 15 ){ :close }
zz.first
=> #<struct TechnicalAnalysis::MovingAverage::EMA time=Wed, 10 Mar 2021, value=0.149524e5> 

```
calculates the _Exponential Moving Average_ on the _close_ property of each item in the 
Enumerator returned by the [contract.eod](https://ib-ruby.github.io/ib-doc/Historical_data.html) method.

The same using a conventional array:
```ruby
u =  z.map( &:close ).each
uu=  u.calculate( :ema, period: 15 ) 
uu.first
=> 0.149524e5 
```


(work in progress)



