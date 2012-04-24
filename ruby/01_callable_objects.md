!SLIDE subsection
# Ruby #

Pavel Pokorný

!SLIDE full-page
# Spustitelné objekty #

* blocks - {...}
* procs and lambdas - Proc.new, proc, lambda
* methods - def, define_method
* _closures_ - obsahují kompletní prostředí pro spuštění (kód, binding)

!SLIDE
# Blocks #

* je možné je vytvořit jen při volání metody
* yield nebo lze získat Proc objekt
* block_given?

!SLIDE
# Blocks #

    @@@ ruby
    def taking_block(&given_proc)
      # Proc.new(&given_proc) # => Proc
      given_proc.class # => Proc
      # lze předat dále
      # another_method(&given_proc)
      # nebo spustit 
      yield(10) # nebo given_proc.call(10)
    end
    
    x = 340
    taking_block { |n| x * n }
    
!SLIDE
# Proc vs. lambda #

* proc - zkratka v 1.8 pro Kernel.lambda v 1.9 pro Proc.new
* lambda je také objekt třídy Proc
* rozdílné chování return
* rozdílná kontrola počtu parametrů (lambda přísnější)
    
!SLIDE
# Methods #

* metody jsou objekty třídy Method
* lze je spustit metodou Method#call()
* scope objektu místo scope místa definice
* lze získat Proc: Method#to_proc()

