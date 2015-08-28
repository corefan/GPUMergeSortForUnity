# GPU Merge Sort for Unity
## Usage

Init:
```csharp
BitonicMergeSort _sort;
ComputeBuffer _keys, _values;

var count = 1 << 10;

_sort = new BitonicMergeSort(compute);
_keys = new ComputeBuffer(count, Marshal.SizeOf(typeof(uint)));
_values = new ComputeBuffer(count, Marshal.SizeOf(typeof(float)));
```

Prepare:
```csharp
var key_data = new uint[count];
var value_data = new float[count];

_keys.SetData(key_data);
for (var i = 0; i < count; i++)
	value_data[i] = Random.value;
_values.SetData(value_data);
```

Sort:
```csharp
_sort.Init(_keys);
_sort.Sort(_keys, _values);
```

Output:
```csharp
_keys.GetData(key_data);

for (var i = 0; i < count; i++)
  Debug.Log(value_data[key_data[i]]);
```

Dispose:
```csharp
void OnDestroy() {
	if (_sort != null)
		_sort.Dispose();
	if (_keys != null)
	  _keys.Dispose();
	 if (_values != null)
	  _values.Dispose();
}
```
