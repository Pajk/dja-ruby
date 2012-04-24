!SLIDE
# Metaprogramování #

* psaní kódu, který vytváří kód
* class, module a def vytváří nový scope
* lze nahradit voláním metody

!SLIDE
# class #
.notes class methods

* přesun do scope definované třídy
* roli self přebírá definovaná třída
* singleton methods, duck typing
* [object model](image/ruby/object_model.png)

!SLIDE
# Nahrazení class a def #

    @@@ ruby
    names = %w[red green blue]
    NewClass = Class.new do
      names.each do |name|
        define_method name do
          puts "I am #{name}"
        end
      end
    end
    
    