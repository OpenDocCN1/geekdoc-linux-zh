# ## Code Efficiency

PHP 5 offers provisions for separating the visible properties and methods of an object from the properties and methods are implemented by the class, by means of the magic `__get()`, `__set()`, and `__call()` methods. Because capitalization matters for variables and properties, you may wish to consider the practice of naming all of your object’s properties with lowercase names, declaring them `private` or `protected`, and then writing routines to provide access via title-case names:

```
class foo
{
    protected $width, $height;

    public function __get($property)
    {
        switch($property)
        {
            case 'Width':
                return $this->width;
            case 'Height':
                return $this->height;
            case 'Area':
                return $this->width*$this->height;
        }
    }

    public function __set($property, $value)
    {
        switch($property, $value)
        {
            case 'Width':
                $this->width = $value;
                return;
        }
    }
}

```

This also gives you finer control over which properties the object’s user may alter or view. Note, for example, that `$object->Height` can be read from but not assigned to—a distinction that would not be possible if you simply made `$object->height` public.

If you make a stylistic distinction between real properties and synthetic ones created via `__get()` and `__set()`, you should make sure that you provide synthetic access to the real properties, and preferably disallow direct access to those properties. This will allow you to create classes that provide exactly the same properties interface regardless of whether each such class uses the same properties internally or not. A complex number object, for example, may provide `$num->Real`, `$num->Imag`, `$num->Arg`, and `$num->Mag`; independently of whether it stores the number as a real part plus an imaginary part and providing the argument and magnitude synthetically, or vice versa.

> *The `__get()` accessor for a synthetic property may include code so that the previous value retrieved is cached in a private property* in case *it is asked for again, with the contents of the cache cleared if and when the property it depends on has altered via* `__set()` *.

When building function and method names up from several words, use either `underscore_separation` or `TitleCase` to show where one word leaves off and the next begins. Opinion is divided over which