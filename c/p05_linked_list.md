# Resizable Array
可变数组
- growable
- get the current size
- access to the elements
## the Interface (函数库)
- Array array_create(int init_size);
- void array_free(Array *a);
- int array_size(const Array *a);
- int* array_at(Array *a, int index);
- void array_inflate(Array *a, int more_size);