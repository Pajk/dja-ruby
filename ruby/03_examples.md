!SLIDE smaller
    @@@ ruby
    module CheckedAttributes
      
      def self.included(base)
        base.extend ClassMethods
      end
      
      module ClassMethods
        def attr_checked(attribute, &validation)
          define_method "#{attribute}=" do |value|
            unless validation.call(value)
              raise 'Invalid attribute'
            end
            instance_variable_set("@#{attribute}", value)
          end
          define_method attribute do
            instance_variable_get "@#{attribute}"
          end
        end
      end
    end
    
    class Person
      include CheckedAttributes
      attr_checked :age { |v| v >= 18 }
    end
    
!SLIDE
# Přidání metody instanci #

    @@@ ruby
    class Array
      def add_method(name, &block)
        meta = class << self; self; end
        meta.send(:define_method, name, &block)
      end
    end
    
    a = [1,2,3]
    a.add_method(:sum) { self.reduce(:+) }
    a.sum # => 6

    
!SLIDE smaller
# Validace parametrů v RoR #
    @@@ ruby
    # v controlleru
    param :regexp_param, /^[0-9]* years/
    param :array_param, [100, "one", "two", 1, 2]
    param :proc_param, lambda { |val| val == "param value"}
    def akce;...;end
    
    ...
    
    def method_added(method_name)
        old_method = instance_method(method_name) 
        define_method(method_name) do |*args|
          # validace parametrů
          old_method.bind(self).call(*args)
        end
      end
    end

!SLIDE small
# Method Missing #
    @@@ ruby
    class Talker
      def method_missing(method, *args, &block)
        if method.to_s =~ /say_(.+)/
          puts $1.capitalize
        else
          super
        end
      end
    
      def respond_to_missing?(method, *)
        method =~ /say_(.+)/ || super
      end
    end
    t = Talker.new
    t.say_what? #=> What?
    
    
!SLIDE
# Dotazy? #

Děkuji za pozornost

Prezentace na githubu [Pajk/dja-ruby](https://github.com/Pajk/dja-ruby)

RoR gem pro validaci a generování dokumentace [Pajk/rails-restapi](https://github.com/Pajk/rails-restapi)