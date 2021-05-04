# 입력 처리

Note: Functions taking `Tensor` arguments can also take anything accepted by [`tf.convert_to_tensor`](framework.md#convert_to_tensor).

\[TOC\]

## Placeholders

TensorFlow provides a placeholder operation that must be fed with data on execution. For more info, see the section on [Feeding data](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/g3doc/how_tos/reading_data/index.md#feeding).

### `tf.placeholder(dtype, shape=None, name=None)` <a id="placeholder"></a>

Inserts a placeholder for a tensor that will be always fed.

**Important**: This tensor will produce an error if evaluated. Its value must be fed using the `feed_dict` optional argument to `Session.run()`, `Tensor.eval()`, or `Operation.run()`.

For example:

```python
x = tf.placeholder(tf.float32, shape=(1024, 1024))
y = tf.matmul(x, x)

with tf.Session() as sess:
  print(sess.run(y))  # ERROR: will fail because x was not fed.

  rand_array = np.random.rand(1024, 1024)
  print(sess.run(y, feed_dict={x: rand_array}))  # Will succeed.
```

**Args:**

* **`dtype`**: The type of elements in the tensor to be fed.
* **`shape`**: The shape of the tensor to be fed \(optional\). If the shape is not

   specified, you can feed a tensor of any shape.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor` that may be used as a handle for feeding a value, but not evaluated directly.

### `tf.placeholder_with_default(input, shape, name=None)` <a id="placeholder_with_default"></a>

A placeholder op that passes though `input` when its output is not fed.

**Args:**

* **`input`**: A `Tensor`. The default value to produce when `output` is not fed.
* **`shape`**: A `tf.TensorShape` or list of `ints`.

   The \(possibly partial\) shape of the tensor.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor`. Has the same type as `input`. A placeholder tensor that defaults to `input` if it is not fed.

For feeding `SparseTensor`s which are composite type, there is a convenience function:

### `tf.sparse_placeholder(dtype, shape=None, name=None)` <a id="sparse_placeholder"></a>

Inserts a placeholder for a sparse tensor that will be always fed.

**Important**: This sparse tensor will produce an error if evaluated. Its value must be fed using the `feed_dict` optional argument to `Session.run()`, `Tensor.eval()`, or `Operation.run()`.

For example:

```python
x = tf.sparse_placeholder(tf.float32)
y = tf.sparse_reduce_sum(x)

with tf.Session() as sess:
  print(sess.run(y))  # ERROR: will fail because x was not fed.

  indices = np.array([[3, 2, 0], [4, 5, 1]], dtype=np.int64)
  values = np.array([1.0, 2.0], dtype=np.float32)
  shape = np.array([7, 9, 2], dtype=np.int64)
  print(sess.run(y, feed_dict={
    x: tf.SparseTensorValue(indices, values, shape)}))  # Will succeed.
  print(sess.run(y, feed_dict={
    x: (indices, values, shape)}))  # Will succeed.

  sp = tf.SparseTensor(indices=indices, values=values, shape=shape)
  sp_value = sp.eval(session)
  print(sess.run(y, feed_dict={x: sp_value}))  # Will succeed.
```

**Args:**

* **`dtype`**: The type of `values` elements in the tensor to be fed.
* **`shape`**: The shape of the tensor to be fed \(optional\). If the shape is not

   specified, you can feed a sparse tensor of any shape.

* **`name`**: A name for prefixing the operations \(optional\).

**Returns:**

A `SparseTensor` that may be used as a handle for feeding a value, but not evaluated directly.

## Readers

TensorFlow provides a set of Reader classes for reading data formats. For more information on inputs and readers, see [Reading data](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/g3doc/how_tos/reading_data/index.md).

### `class tf.ReaderBase` <a id="ReaderBase"></a>

Base class for different Reader types, that produce a record every step.

Conceptually, Readers convert string 'work units' into records \(key, value pairs\). Typically the 'work units' are filenames and the records are extracted from the contents of those files. We want a single record produced per step, but a work unit can correspond to many records.

Therefore we introduce some decoupling using a queue. The queue contains the work units and the Reader dequeues from the queue when it is asked to produce a record \(via Read\(\)\) but it has finished the last work unit.

#### `tf.ReaderBase.__init__(reader_ref, supports_serialize=False)` <a id="ReaderBase.__init__"></a>

Creates a new ReaderBase.

**Args:**

* **`reader_ref`**: The operation that implements the reader.
* **`supports_serialize`**: True if the reader implementation can

   serialize its state.

#### `tf.ReaderBase.num_records_produced(name=None)` <a id="ReaderBase.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.ReaderBase.num_work_units_completed(name=None)` <a id="ReaderBase.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.ReaderBase.read(queue, name=None)` <a id="ReaderBase.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.ReaderBase.read_up_to(queue, num_records, name=None)` <a id="ReaderBase.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.ReaderBase.reader_ref` <a id="ReaderBase.reader_ref"></a>

Op that implements the reader.

#### `tf.ReaderBase.reset(name=None)` <a id="ReaderBase.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.ReaderBase.restore_state(state, name=None)` <a id="ReaderBase.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.ReaderBase.serialize_state(name=None)` <a id="ReaderBase.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.ReaderBase.supports_serialize` <a id="ReaderBase.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

### `class tf.TextLineReader` <a id="TextLineReader"></a>

A Reader that outputs the lines of a file delimited by newlines.

Newlines are stripped from the output. See ReaderBase for supported methods.

#### `tf.TextLineReader.__init__(skip_header_lines=None, name=None)` <a id="TextLineReader.__init__"></a>

Create a TextLineReader.

**Args:**

* **`skip_header_lines`**: An optional int. Defaults to 0.  Number of lines

   to skip from the beginning of every file.

* **`name`**: A name for the operation \(optional\).

#### `tf.TextLineReader.num_records_produced(name=None)` <a id="TextLineReader.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.TextLineReader.num_work_units_completed(name=None)` <a id="TextLineReader.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.TextLineReader.read(queue, name=None)` <a id="TextLineReader.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.TextLineReader.read_up_to(queue, num_records, name=None)` <a id="TextLineReader.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.TextLineReader.reader_ref` <a id="TextLineReader.reader_ref"></a>

Op that implements the reader.

#### `tf.TextLineReader.reset(name=None)` <a id="TextLineReader.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.TextLineReader.restore_state(state, name=None)` <a id="TextLineReader.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.TextLineReader.serialize_state(name=None)` <a id="TextLineReader.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.TextLineReader.supports_serialize` <a id="TextLineReader.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

### `class tf.WholeFileReader` <a id="WholeFileReader"></a>

A Reader that outputs the entire contents of a file as a value.

To use, enqueue filenames in a Queue. The output of Read will be a filename \(key\) and the contents of that file \(value\).

See ReaderBase for supported methods.

#### `tf.WholeFileReader.__init__(name=None)` <a id="WholeFileReader.__init__"></a>

Create a WholeFileReader.

**Args:**

* **`name`**: A name for the operation \(optional\).

#### `tf.WholeFileReader.num_records_produced(name=None)` <a id="WholeFileReader.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.WholeFileReader.num_work_units_completed(name=None)` <a id="WholeFileReader.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.WholeFileReader.read(queue, name=None)` <a id="WholeFileReader.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.WholeFileReader.read_up_to(queue, num_records, name=None)` <a id="WholeFileReader.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.WholeFileReader.reader_ref` <a id="WholeFileReader.reader_ref"></a>

Op that implements the reader.

#### `tf.WholeFileReader.reset(name=None)` <a id="WholeFileReader.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.WholeFileReader.restore_state(state, name=None)` <a id="WholeFileReader.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.WholeFileReader.serialize_state(name=None)` <a id="WholeFileReader.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.WholeFileReader.supports_serialize` <a id="WholeFileReader.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

### `class tf.IdentityReader` <a id="IdentityReader"></a>

A Reader that outputs the queued work as both the key and value.

To use, enqueue strings in a Queue. Read will take the front work string and output \(work, work\).

See ReaderBase for supported methods.

#### `tf.IdentityReader.__init__(name=None)` <a id="IdentityReader.__init__"></a>

Create a IdentityReader.

**Args:**

* **`name`**: A name for the operation \(optional\).

#### `tf.IdentityReader.num_records_produced(name=None)` <a id="IdentityReader.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.IdentityReader.num_work_units_completed(name=None)` <a id="IdentityReader.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.IdentityReader.read(queue, name=None)` <a id="IdentityReader.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.IdentityReader.read_up_to(queue, num_records, name=None)` <a id="IdentityReader.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.IdentityReader.reader_ref` <a id="IdentityReader.reader_ref"></a>

Op that implements the reader.

#### `tf.IdentityReader.reset(name=None)` <a id="IdentityReader.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.IdentityReader.restore_state(state, name=None)` <a id="IdentityReader.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.IdentityReader.serialize_state(name=None)` <a id="IdentityReader.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.IdentityReader.supports_serialize` <a id="IdentityReader.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

### `class tf.TFRecordReader` <a id="TFRecordReader"></a>

A Reader that outputs the records from a TFRecords file.

See ReaderBase for supported methods.

#### `tf.TFRecordReader.__init__(name=None)` <a id="TFRecordReader.__init__"></a>

Create a TFRecordReader.

**Args:**

* **`name`**: A name for the operation \(optional\).

#### `tf.TFRecordReader.num_records_produced(name=None)` <a id="TFRecordReader.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.TFRecordReader.num_work_units_completed(name=None)` <a id="TFRecordReader.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.TFRecordReader.read(queue, name=None)` <a id="TFRecordReader.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.TFRecordReader.read_up_to(queue, num_records, name=None)` <a id="TFRecordReader.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.TFRecordReader.reader_ref` <a id="TFRecordReader.reader_ref"></a>

Op that implements the reader.

#### `tf.TFRecordReader.reset(name=None)` <a id="TFRecordReader.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.TFRecordReader.restore_state(state, name=None)` <a id="TFRecordReader.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.TFRecordReader.serialize_state(name=None)` <a id="TFRecordReader.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.TFRecordReader.supports_serialize` <a id="TFRecordReader.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

### `class tf.FixedLengthRecordReader` <a id="FixedLengthRecordReader"></a>

A Reader that outputs fixed-length records from a file.

See ReaderBase for supported methods.

#### `tf.FixedLengthRecordReader.__init__(record_bytes, header_bytes=None, footer_bytes=None, name=None)` <a id="FixedLengthRecordReader.__init__"></a>

Create a FixedLengthRecordReader.

**Args:**

* **`record_bytes`**: An int.
* **`header_bytes`**: An optional int. Defaults to 0.
* **`footer_bytes`**: An optional int. Defaults to 0.
* **`name`**: A name for the operation \(optional\).

#### `tf.FixedLengthRecordReader.num_records_produced(name=None)` <a id="FixedLengthRecordReader.num_records_produced"></a>

Returns the number of records this reader has produced.

This is the same as the number of Read executions that have succeeded.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.FixedLengthRecordReader.num_work_units_completed(name=None)` <a id="FixedLengthRecordReader.num_work_units_completed"></a>

Returns the number of work units this reader has finished processing.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

An int64 Tensor.

#### `tf.FixedLengthRecordReader.read(queue, name=None)` <a id="FixedLengthRecordReader.read"></a>

Returns the next record \(key, value pair\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g. when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(key, value\).

* **`key`**: A string scalar Tensor.
* **`value`**: A string scalar Tensor.

#### `tf.FixedLengthRecordReader.read_up_to(queue, num_records, name=None)` <a id="FixedLengthRecordReader.read_up_to"></a>

Returns up to num\_records \(key, value pairs\) produced by a reader.

Will dequeue a work unit from queue if necessary \(e.g., when the Reader needs to start reading from a new file since it has finished with the previous file\).

**Args:**

* **`queue`**: A Queue or a mutable string Tensor representing a handle

   to a Queue, with string work items.

* **`num_records`**: Number of records to read.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A tuple of Tensors \(keys, values\).

* **`keys`**: A 1-D string Tensor.
* **`values`**: A 1-D string Tensor.

#### `tf.FixedLengthRecordReader.reader_ref` <a id="FixedLengthRecordReader.reader_ref"></a>

Op that implements the reader.

#### `tf.FixedLengthRecordReader.reset(name=None)` <a id="FixedLengthRecordReader.reset"></a>

Restore a reader to its initial clean state.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.FixedLengthRecordReader.restore_state(state, name=None)` <a id="FixedLengthRecordReader.restore_state"></a>

Restore a reader to a previously saved state.

Not all Readers support being restored, so this can produce an Unimplemented error.

**Args:**

* **`state`**: A string Tensor.

   Result of a SerializeState of a Reader with matching type.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The created Operation.

#### `tf.FixedLengthRecordReader.serialize_state(name=None)` <a id="FixedLengthRecordReader.serialize_state"></a>

Produce a string tensor that encodes the state of a reader.

Not all Readers support being serialized, so this can produce an Unimplemented error.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A string Tensor.

#### `tf.FixedLengthRecordReader.supports_serialize` <a id="FixedLengthRecordReader.supports_serialize"></a>

Whether the Reader implementation can serialize its state.

## Converting

TensorFlow provides several operations that you can use to convert various data formats into tensors.

### `tf.decode_csv(records, record_defaults, field_delim=None, name=None)` <a id="decode_csv"></a>

Convert CSV records to tensors. Each column maps to one tensor.

RFC 4180 format is expected for the CSV records. \([https://tools.ietf.org/html/rfc4180](https://tools.ietf.org/html/rfc4180)\) Note that we allow leading and trailing spaces with int or float field.

**Args:**

* **`records`**: A `Tensor` of type `string`.

   Each string is a record/row in the csv and all records should have

   the same format.

* **`record_defaults`**: A list of `Tensor` objects with types from: `float32`, `int32`, `int64`, `string`.

   One tensor per column of the input record, with either a

   scalar default value for that column or empty if the column is required.

* **`field_delim`**: An optional `string`. Defaults to `","`.

   delimiter to separate fields in a record.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A list of `Tensor` objects. Has the same type as `record_defaults`. Each tensor will have the same shape as records.

### `tf.decode_raw(bytes, out_type, little_endian=None, name=None)` <a id="decode_raw"></a>

Reinterpret the bytes of a string as a vector of numbers.

**Args:**

* **`bytes`**: A `Tensor` of type `string`.

   All the elements must have the same length.

* **`out_type`**: A `tf.DType` from: `tf.float32, tf.float64, tf.int32, tf.uint8, tf.int16, tf.int8, tf.int64`.
* **`little_endian`**: An optional `bool`. Defaults to `True`.

   Whether the input `bytes` are in little-endian order.

   Ignored for `out_type` values that are stored in a single byte like

   `uint8`.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor` of type `out_type`. A Tensor with one more dimension than the input `bytes`. The added dimension will have size equal to the length of the elements of `bytes` divided by the number of bytes to represent `out_type`.

### Example protocol buffer

TensorFlow's [recommended format for training examples](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/g3doc/how_tos/reading_data/index.md#standard-tensorflow-format) is serialized `Example` protocol buffers, [described here](https://www.tensorflow.org/code/tensorflow/core/example/example.proto). They contain `Features`, [described here](https://www.tensorflow.org/code/tensorflow/core/example/feature.proto).

### `class tf.VarLenFeature` <a id="VarLenFeature"></a>

Configuration for parsing a variable-length input feature.

Fields: dtype: Data type of input.

#### `tf.VarLenFeature.dtype` <a id="VarLenFeature.dtype"></a>

Alias for field number 0

### `class tf.FixedLenFeature` <a id="FixedLenFeature"></a>

Configuration for parsing a fixed-length input feature.

To treat sparse input as dense, provide a `default_value`; otherwise, the parse functions will fail on any examples missing this feature.

Fields: shape: Shape of input data. dtype: Data type of input. default\_value: Value to be used if an example is missing this feature. It must be compatible with `dtype`.

#### `tf.FixedLenFeature.default_value` <a id="FixedLenFeature.default_value"></a>

Alias for field number 2

#### `tf.FixedLenFeature.dtype` <a id="FixedLenFeature.dtype"></a>

Alias for field number 1

#### `tf.FixedLenFeature.shape` <a id="FixedLenFeature.shape"></a>

Alias for field number 0

### `class tf.FixedLenSequenceFeature` <a id="FixedLenSequenceFeature"></a>

Configuration for a dense input feature in a sequence item.

To treat a sparse input as dense, provide `allow_missing=True`; otherwise, the parse functions will fail on any examples missing this feature.

Fields: shape: Shape of input data. dtype: Data type of input. allow\_missing: Whether to allow this feature to be missing from a feature list item.

#### `tf.FixedLenSequenceFeature.allow_missing` <a id="FixedLenSequenceFeature.allow_missing"></a>

Alias for field number 2

#### `tf.FixedLenSequenceFeature.dtype` <a id="FixedLenSequenceFeature.dtype"></a>

Alias for field number 1

#### `tf.FixedLenSequenceFeature.shape` <a id="FixedLenSequenceFeature.shape"></a>

Alias for field number 0

### `tf.parse_example(serialized, features, name=None, example_names=None)` <a id="parse_example"></a>

Parses `Example` protos into a `dict` of tensors.

Parses a number of serialized \[`Example`\] \([https://www.tensorflow.org/code/tensorflow/core/example/example.proto](https://www.tensorflow.org/code/tensorflow/core/example/example.proto)\) protos given in `serialized`.

`example_names` may contain descriptive names for the corresponding serialized protos. These may be useful for debugging purposes, but they have no effect on the output. If not `None`, `example_names` must be the same length as `serialized`.

This op parses serialized examples into a dictionary mapping keys to `Tensor` and `SparseTensor` objects. `features` is a dict from keys to `VarLenFeature` and `FixedLenFeature` objects. Each `VarLenFeature` is mapped to a `SparseTensor`, and each `FixedLenFeature` is mapped to a `Tensor`.

Each `VarLenFeature` maps to a `SparseTensor` of the specified type representing a ragged matrix. Its indices are `[batch, index]` where `batch` is the batch entry the value is from in `serialized`, and `index` is the value's index in the list of values associated with that feature and example.

Each `FixedLenFeature` `df` maps to a `Tensor` of the specified type \(or `tf.float32` if not specified\) and shape `(serialized.size(),) + df.shape`.

`FixedLenFeature` entries with a `default_value` are optional. With no default value, we will fail if that `Feature` is missing from any example in `serialized`.

Examples:

For example, if one expects a `tf.float32` sparse feature `ft` and three serialized `Example`s are provided:

```text
serialized = [
  features
    { feature { key: "ft" value { float_list { value: [1.0, 2.0] } } } },
  features
    { feature []},
  features
    { feature { key: "ft" value { float_list { value: [3.0] } } }
]
```

then the output will look like:

```text
{"ft": SparseTensor(indices=[[0, 0], [0, 1], [2, 0]],
                    values=[1.0, 2.0, 3.0],
                    shape=(3, 2)) }
```

Given two `Example` input protos in `serialized`:

```text
[
  features {
    feature { key: "kw" value { bytes_list { value: [ "knit", "big" ] } } }
    feature { key: "gps" value { float_list { value: [] } } }
  },
  features {
    feature { key: "kw" value { bytes_list { value: [ "emmy" ] } } }
    feature { key: "dank" value { int64_list { value: [ 42 ] } } }
    feature { key: "gps" value { } }
  }
]
```

And arguments

```text
example_names: ["input0", "input1"],
features: {
    "kw": VarLenFeature(tf.string),
    "dank": VarLenFeature(tf.int64),
    "gps": VarLenFeature(tf.float32),
}
```

Then the output is a dictionary:

```python
{
  "kw": SparseTensor(
      indices=[[0, 0], [0, 1], [1, 0]],
      values=["knit", "big", "emmy"]
      shape=[2, 2]),
  "dank": SparseTensor(
      indices=[[1, 0]],
      values=[42],
      shape=[2, 1]),
  "gps": SparseTensor(
      indices=[],
      values=[],
      shape=[2, 0]),
}
```

For dense results in two serialized `Example`s:

```text
[
  features {
    feature { key: "age" value { int64_list { value: [ 0 ] } } }
    feature { key: "gender" value { bytes_list { value: [ "f" ] } } }
   },
   features {
    feature { key: "age" value { int64_list { value: [] } } }
    feature { key: "gender" value { bytes_list { value: [ "f" ] } } }
  }
]
```

We can use arguments:

```text
example_names: ["input0", "input1"],
features: {
    "age": FixedLenFeature([], dtype=tf.int64, default_value=-1),
    "gender": FixedLenFeature([], dtype=tf.string),
}
```

And the expected output is:

```python
{
  "age": [[0], [-1]],
  "gender": [["f"], ["f"]],
}
```

**Args:**

* **`serialized`**: A vector \(1-D Tensor\) of strings, a batch of binary

   serialized `Example` protos.

* **`features`**: A `dict` mapping feature keys to `FixedLenFeature` or

   `VarLenFeature` values.

* **`name`**: A name for this operation \(optional\).
* **`example_names`**: A vector \(1-D Tensor\) of strings \(optional\), the names of

   the serialized protos in the batch.

**Returns:**

A `dict` mapping feature keys to `Tensor` and `SparseTensor` values.

**Raises:**

* **`ValueError`**: if any feature is invalid.

### `tf.parse_single_example(serialized, features, name=None, example_names=None)` <a id="parse_single_example"></a>

Parses a single `Example` proto.

Similar to `parse_example`, except:

For dense tensors, the returned `Tensor` is identical to the output of `parse_example`, except there is no batch dimension, the output shape is the same as the shape given in `dense_shape`.

For `SparseTensor`s, the first \(batch\) column of the indices matrix is removed \(the indices matrix is a column vector\), the values vector is unchanged, and the first \(`batch_size`\) entry of the shape vector is removed \(it is now a single element vector\).

**Args:**

* **`serialized`**: A scalar string Tensor, a single serialized Example.

   See `_parse_single_example_raw` documentation for more details.

* **`features`**: A `dict` mapping feature keys to `FixedLenFeature` or

   `VarLenFeature` values.

* **`name`**: A name for this operation \(optional\).
* **`example_names`**: \(Optional\) A scalar string Tensor, the associated name.

   See `_parse_single_example_raw` documentation for more details.

**Returns:**

A `dict` mapping feature keys to `Tensor` and `SparseTensor` values.

**Raises:**

* **`ValueError`**: if any feature is invalid.

### `tf.decode_json_example(json_examples, name=None)` <a id="decode_json_example"></a>

Convert JSON-encoded Example records to binary protocol buffer strings.

This op translates a tensor containing Example records, encoded using the [standard JSON mapping](https://developers.google.com/protocol-buffers/docs/proto3#json), into a tensor containing the same records encoded as binary protocol buffers. The resulting tensor can then be fed to any of the other Example-parsing ops.

**Args:**

* **`json_examples`**: A `Tensor` of type `string`.

   Each string is a JSON object serialized according to the JSON

   mapping of the Example proto.

* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor` of type `string`. Each string is a binary Example protocol buffer corresponding to the respective element of `json_examples`.

## Queues

TensorFlow provides several implementations of 'Queues', which are structures within the TensorFlow computation graph to stage pipelines of tensors together. The following describe the basic Queue interface and some implementations. To see an example use, see [Threading and Queues](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/g3doc/how_tos/threading_and_queues/index.md).

### `class tf.QueueBase` <a id="QueueBase"></a>

Base class for queue implementations.

A queue is a TensorFlow data structure that stores tensors across multiple steps, and exposes operations that enqueue and dequeue tensors.

Each queue element is a tuple of one or more tensors, where each tuple component has a static dtype, and may have a static shape. The queue implementations support versions of enqueue and dequeue that handle single elements, versions that support enqueuing and dequeuing a batch of elements at once.

See [`tf.FIFOQueue`](io_ops.md#FIFOQueue) and [`tf.RandomShuffleQueue`](io_ops.md#RandomShuffleQueue) for concrete implementations of this class, and instructions on how to create them.

#### `tf.QueueBase.enqueue(vals, name=None)` <a id="QueueBase.enqueue"></a>

Enqueues one element to this queue.

If the queue is full when this operation executes, it will block until the element has been enqueued.

At runtime, this operation may raise an error if the queue is [closed](io_ops.md#QueueBase.close) before or during its execution. If the queue is closed before this operation runs, `tf.errors.AbortedError` will be raised. If this operation is blocked, and either \(i\) the queue is closed by a close operation with `cancel_pending_enqueues=True`, or \(ii\) the session is [closed](client.md#Session.close), `tf.errors.CancelledError` will be raised.

**Args:**

* **`vals`**: A tensor, a list or tuple of tensors, or a dictionary containing

   the values to enqueue.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The operation that enqueues a new tuple of tensors to the queue.

#### `tf.QueueBase.enqueue_many(vals, name=None)` <a id="QueueBase.enqueue_many"></a>

Enqueues zero or more elements to this queue.

This operation slices each component tensor along the 0th dimension to make multiple queue elements. All of the tensors in `vals` must have the same size in the 0th dimension.

If the queue is full when this operation executes, it will block until all of the elements have been enqueued.

At runtime, this operation may raise an error if the queue is [closed](io_ops.md#QueueBase.close) before or during its execution. If the queue is closed before this operation runs, `tf.errors.AbortedError` will be raised. If this operation is blocked, and either \(i\) the queue is closed by a close operation with `cancel_pending_enqueues=True`, or \(ii\) the session is [closed](client.md#Session.close), `tf.errors.CancelledError` will be raised.

**Args:**

* **`vals`**: A tensor, a list or tuple of tensors, or a dictionary

   from which the queue elements are taken.

* **`name`**: A name for the operation \(optional\).

**Returns:**

The operation that enqueues a batch of tuples of tensors to the queue.

#### `tf.QueueBase.dequeue(name=None)` <a id="QueueBase.dequeue"></a>

Dequeues one element from this queue.

If the queue is empty when this operation executes, it will block until there is an element to dequeue.

At runtime, this operation may raise an error if the queue is [closed](io_ops.md#QueueBase.close) before or during its execution. If the queue is closed, the queue is empty, and there are no pending enqueue operations that can fulfil this request, `tf.errors.OutOfRangeError` will be raised. If the session is [closed](client.md#Session.close), `tf.errors.CancelledError` will be raised.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

The tuple of tensors that was dequeued.

#### `tf.QueueBase.dequeue_many(n, name=None)` <a id="QueueBase.dequeue_many"></a>

Dequeues and concatenates `n` elements from this queue.

This operation concatenates queue-element component tensors along the 0th dimension to make a single component tensor. All of the components in the dequeued tuple will have size `n` in the 0th dimension.

If the queue is closed and there are less than `n` elements left, then an `OutOfRange` exception is raised.

At runtime, this operation may raise an error if the queue is [closed](io_ops.md#QueueBase.close) before or during its execution. If the queue is closed, the queue contains fewer than `n` elements, and there are no pending enqueue operations that can fulfil this request, `tf.errors.OutOfRangeError` will be raised. If the session is [closed](client.md#Session.close), `tf.errors.CancelledError` will be raised.

**Args:**

* **`n`**: A scalar `Tensor` containing the number of elements to dequeue.
* **`name`**: A name for the operation \(optional\).

**Returns:**

The tuple of concatenated tensors that was dequeued.

#### `tf.QueueBase.size(name=None)` <a id="QueueBase.size"></a>

Compute the number of elements in this queue.

**Args:**

* **`name`**: A name for the operation \(optional\).

**Returns:**

A scalar tensor containing the number of elements in this queue.

#### `tf.QueueBase.close(cancel_pending_enqueues=False, name=None)` <a id="QueueBase.close"></a>

Closes this queue.

This operation signals that no more elements will be enqueued in the given queue. Subsequent `enqueue` and `enqueue_many` operations will fail. Subsequent `dequeue` and `dequeue_many` operations will continue to succeed if sufficient elements remain in the queue. Subsequent `dequeue` and `dequeue_many` operations that would block will fail immediately.

If `cancel_pending_enqueues` is `True`, all pending requests will also be cancelled.

**Args:**

* **`cancel_pending_enqueues`**: \(Optional.\) A boolean, defaulting to

   `False` \(described above\).

* **`name`**: A name for the operation \(optional\).

**Returns:**

The operation that closes the queue.

#### Other Methods

#### `tf.QueueBase.__init__(dtypes, shapes, names, queue_ref)` <a id="QueueBase.__init__"></a>

Constructs a queue object from a queue reference.

The two optional lists, `shapes` and `names`, must be of the same length as `dtypes` if provided. The values at a given index `i` indicate the shape and name to use for the corresponding queue component in `dtypes`.

**Args:**

* **`dtypes`**: A list of types.  The length of dtypes must equal the number

   of tensors in each element.

* **`shapes`**: Constraints on the shapes of tensors in an element:

   A list of shape tuples or None. This list is the same length

   as dtypes.  If the shape of any tensors in the element are constrained,

   all must be; shapes can be None if the shapes should not be constrained.

* **`names`**: Optional list of names.  If provided, the `enqueue()` and

   `dequeue()` methods will use dictionaries with these names as keys.

   Must be None or a list or tuple of the same length as `dtypes`.

* **`queue_ref`**: The queue reference, i.e. the output of the queue op.

**Raises:**

* **`ValueError`**: If one of the arguments is invalid.

#### `tf.QueueBase.dequeue_up_to(n, name=None)` <a id="QueueBase.dequeue_up_to"></a>

Dequeues and concatenates `n` elements from this queue.

**Note** This operation is not supported by all queues. If a queue does not support DequeueUpTo, then a `tf.errors.UnimplementedError` is raised.

This operation concatenates queue-element component tensors along the 0th dimension to make a single component tensor. If the queue has not been closed, all of the components in the dequeued tuple will have size `n` in the 0th dimension.

If the queue is closed and there are more than `0` but fewer than `n` elements remaining, then instead of raising a `tf.errors.OutOfRangeError` like [`dequeue_many`](io_ops.md#QueueBase.dequeue_many), the remaining elements are returned immediately. If the queue is closed and there are `0` elements left in the queue, then a `tf.errors.OutOfRangeError` is raised just like in `dequeue_many`. Otherwise the behavior is identical to `dequeue_many`.

**Args:**

* **`n`**: A scalar `Tensor` containing the number of elements to dequeue.
* **`name`**: A name for the operation \(optional\).

**Returns:**

The tuple of concatenated tensors that was dequeued.

#### `tf.QueueBase.dtypes` <a id="QueueBase.dtypes"></a>

The list of dtypes for each component of a queue element.

#### `tf.QueueBase.from_list(index, queues)` <a id="QueueBase.from_list"></a>

Create a queue using the queue reference from `queues[index]`.

**Args:**

* **`index`**: An integer scalar tensor that determines the input that gets

   selected.

* **`queues`**: A list of `QueueBase` objects.

**Returns:**

A `QueueBase` object.

**Raises:**

* **`TypeError`**: When `queues` is not a list of `QueueBase` objects,

   or when the data types of `queues` are not all the same.

#### `tf.QueueBase.name` <a id="QueueBase.name"></a>

The name of the underlying queue.

#### `tf.QueueBase.names` <a id="QueueBase.names"></a>

The list of names for each component of a queue element.

#### `tf.QueueBase.queue_ref` <a id="QueueBase.queue_ref"></a>

The underlying queue reference.

### `class tf.FIFOQueue` <a id="FIFOQueue"></a>

A queue implementation that dequeues elements in first-in-first out order.

See [`tf.QueueBase`](io_ops.md#QueueBase) for a description of the methods on this class.

#### `tf.FIFOQueue.__init__(capacity, dtypes, shapes=None, names=None, shared_name=None, name='fifo_queue')` <a id="FIFOQueue.__init__"></a>

Creates a queue that dequeues elements in a first-in first-out order.

A `FIFOQueue` has bounded capacity; supports multiple concurrent producers and consumers; and provides exactly-once delivery.

A `FIFOQueue` holds a list of up to `capacity` elements. Each element is a fixed-length tuple of tensors whose dtypes are described by `dtypes`, and whose shapes are optionally described by the `shapes` argument.

If the `shapes` argument is specified, each component of a queue element must have the respective fixed shape. If it is unspecified, different queue elements may have different shapes, but the use of `dequeue_many` is disallowed.

**Args:**

* **`capacity`**: An integer. The upper bound on the number of elements

   that may be stored in this queue.

* **`dtypes`**: A list of `DType` objects. The length of `dtypes` must equal

   the number of tensors in each queue element.

* **`shapes`**: \(Optional.\) A list of fully-defined `TensorShape` objects

   with the same length as `dtypes`, or `None`.

* **`names`**: \(Optional.\) A list of string naming the components in the queue

   with the same length as `dtypes`, or `None`.  If specified the dequeue

   methods return a dictionary with the names as keys.

* **`shared_name`**: \(Optional.\) If non-empty, this queue will be shared under

   the given name across multiple sessions.

* **`name`**: Optional name for the queue operation.

### `class tf.PaddingFIFOQueue` <a id="PaddingFIFOQueue"></a>

A FIFOQueue that supports batching variable-sized tensors by padding.

A `PaddingFIFOQueue` may contain components with dynamic shape, while also supporting `dequeue_many`. See the constructor for more details.

See [`tf.QueueBase`](io_ops.md#QueueBase) for a description of the methods on this class.

#### `tf.PaddingFIFOQueue.__init__(capacity, dtypes, shapes, names=None, shared_name=None, name='padding_fifo_queue')` <a id="PaddingFIFOQueue.__init__"></a>

Creates a queue that dequeues elements in a first-in first-out order.

A `PaddingFIFOQueue` has bounded capacity; supports multiple concurrent producers and consumers; and provides exactly-once delivery.

A `PaddingFIFOQueue` holds a list of up to `capacity` elements. Each element is a fixed-length tuple of tensors whose dtypes are described by `dtypes`, and whose shapes are described by the `shapes` argument.

The `shapes` argument must be specified; each component of a queue element must have the respective shape. Shapes of fixed rank but variable size are allowed by setting any shape dimension to None. In this case, the inputs' shape may vary along the given dimension, and `dequeue_many` will pad the given dimension with zeros up to the maximum shape of all elements in the given batch.

**Args:**

* **`capacity`**: An integer. The upper bound on the number of elements

   that may be stored in this queue.

* **`dtypes`**: A list of `DType` objects. The length of `dtypes` must equal

   the number of tensors in each queue element.

* **`shapes`**: A list of `TensorShape` objects, with the same length as

   `dtypes`.  Any dimension in the `TensorShape` containing value

   `None` is dynamic and allows values to be enqueued with

    variable size in that dimension.

* **`names`**: \(Optional.\) A list of string naming the components in the queue

   with the same length as `dtypes`, or `None`.  If specified the dequeue

   methods return a dictionary with the names as keys.

* **`shared_name`**: \(Optional.\) If non-empty, this queue will be shared under

   the given name across multiple sessions.

* **`name`**: Optional name for the queue operation.

**Raises:**

* **`ValueError`**: If shapes is not a list of shapes, or the lengths of dtypes

   and shapes do not match, or if names is specified and the lengths of

   dtypes and names do not match.

### `class tf.RandomShuffleQueue` <a id="RandomShuffleQueue"></a>

A queue implementation that dequeues elements in a random order.

See [`tf.QueueBase`](io_ops.md#QueueBase) for a description of the methods on this class.

#### `tf.RandomShuffleQueue.__init__(capacity, min_after_dequeue, dtypes, shapes=None, names=None, seed=None, shared_name=None, name='random_shuffle_queue')` <a id="RandomShuffleQueue.__init__"></a>

Create a queue that dequeues elements in a random order.

A `RandomShuffleQueue` has bounded capacity; supports multiple concurrent producers and consumers; and provides exactly-once delivery.

A `RandomShuffleQueue` holds a list of up to `capacity` elements. Each element is a fixed-length tuple of tensors whose dtypes are described by `dtypes`, and whose shapes are optionally described by the `shapes` argument.

If the `shapes` argument is specified, each component of a queue element must have the respective fixed shape. If it is unspecified, different queue elements may have different shapes, but the use of `dequeue_many` is disallowed.

The `min_after_dequeue` argument allows the caller to specify a minimum number of elements that will remain in the queue after a `dequeue` or `dequeue_many` operation completes, to ensure a minimum level of mixing of elements. This invariant is maintained by blocking those operations until sufficient elements have been enqueued. The `min_after_dequeue` argument is ignored after the queue has been closed.

**Args:**

* **`capacity`**: An integer. The upper bound on the number of elements

   that may be stored in this queue.

* **`min_after_dequeue`**: An integer \(described above\).
* **`dtypes`**: A list of `DType` objects. The length of `dtypes` must equal

   the number of tensors in each queue element.

* **`shapes`**: \(Optional.\) A list of fully-defined `TensorShape` objects

   with the same length as `dtypes`, or `None`.

* **`names`**: \(Optional.\) A list of string naming the components in the queue

   with the same length as `dtypes`, or `None`.  If specified the dequeue

   methods return a dictionary with the names as keys.

* **`seed`**: A Python integer. Used to create a random seed. See

   [`set_random_seed`](constant_op.md#set_random_seed)

   for behavior.

* **`shared_name`**: \(Optional.\) If non-empty, this queue will be shared under

   the given name across multiple sessions.

* **`name`**: Optional name for the queue operation.

## Dealing with the filesystem

### `tf.matching_files(pattern, name=None)` <a id="matching_files"></a>

Returns the set of files matching a pattern.

Note that this routine only supports wildcard characters in the basename portion of the pattern, not in the directory portion.

**Args:**

* **`pattern`**: A `Tensor` of type `string`. A \(scalar\) shell wildcard pattern.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor` of type `string`. A vector of matching filenames.

### `tf.read_file(filename, name=None)` <a id="read_file"></a>

Reads and outputs the entire contents of the input filename.

**Args:**

* **`filename`**: A `Tensor` of type `string`.
* **`name`**: A name for the operation \(optional\).

**Returns:**

A `Tensor` of type `string`.

## Input pipeline

TensorFlow functions for setting up an input-prefetching pipeline. Please see the [reading data how-to](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/g3doc/how_tos/reading_data/index.md) for context.

### Beginning of an input pipeline

The "producer" functions add a queue to the graph and a corresponding `QueueRunner` for running the subgraph that fills that queue.

### `tf.train.match_filenames_once(pattern, name=None)` <a id="match_filenames_once"></a>

Save the list of files matching pattern, so it is only computed once.

**Args:**

* **`pattern`**: A file pattern \(glob\).
* **`name`**: A name for the operations \(optional\).

**Returns:**

A variable that is initialized to the list of files matching pattern.

### `tf.train.limit_epochs(tensor, num_epochs=None, name=None)` <a id="limit_epochs"></a>

Returns tensor `num_epochs` times and then raises an `OutOfRange` error.

**Args:**

* **`tensor`**: Any `Tensor`.
* **`num_epochs`**: A positive integer \(optional\).  If specified, limits the number

   of steps the output tensor may be evaluated.

* **`name`**: A name for the operations \(optional\).

**Returns:**

tensor or `OutOfRange`.

**Raises:**

* **`ValueError`**: if `num_epochs` is invalid.

### `tf.train.input_producer(input_tensor, element_shape=None, num_epochs=None, shuffle=True, seed=None, capacity=32, shared_name=None, summary_name=None, name=None)` <a id="input_producer"></a>

Output the rows of `input_tensor` to a queue for an input pipeline.

**Args:**

* **`input_tensor`**: A tensor with the rows to produce. Must be at

   one-dimensional. Must either have a fully-defined shape, or

   `element_shape` must be defined.

* **`element_shape`**: \(Optional.\) A `TensorShape` representing the shape of a

   row of `input_tensor`, if it cannot be inferred.

* **`num_epochs`**: \(Optional.\) An integer. If specified `input_producer` produces

   each row of `input_tensor` `num_epochs` times before generating an

   `OutOfRange` error. If not specified, `input_producer` can cycle through

   the rows of `input_tensor` an unlimited number of times.

* **`shuffle`**: \(Optional.\) A boolean. If true, the rows are randomly shuffled

   within each eopch.

* **`seed`**: \(Optional.\) An integer. The seed to use if `shuffle` is true.
* **`capacity`**: \(Optional.\) The capacity of the queue to be used for buffering

   the input.

* **`shared_name`**: \(Optional.\) If set, this queue will be shared under the given

   name across multiple sessions.

* **`summary_name`**: \(Optional.\) If set, a scalar summary for the current queue

   size will be generated, using this name as part of the tag.

* **`name`**: \(Optional.\) A name for queue.

**Returns:**

A queue with the output rows. A `QueueRunner` for the queue is added to the current `QUEUE_RUNNER` collection of the current graph.

**Raises:**

* **`ValueError`**: If the shape of the input cannot be inferred from the arguments.

### `tf.train.range_input_producer(limit, num_epochs=None, shuffle=True, seed=None, capacity=32, shared_name=None, name=None)` <a id="range_input_producer"></a>

Produces the integers from 0 to limit-1 in a queue.

**Args:**

* **`limit`**: An int32 scalar tensor.
* **`num_epochs`**: An integer \(optional\). If specified, `range_input_producer`

   produces each integer `num_epochs` times before generating an

   OutOfRange error. If not specified, `range_input_producer` can cycle

   through the integers an unlimited number of times.

* **`shuffle`**: Boolean. If true, the integers are randomly shuffled within each

   epoch.

* **`seed`**: An integer \(optional\). Seed used if shuffle == True.
* **`capacity`**: An integer. Sets the queue capacity.
* **`shared_name`**: \(optional\). If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: A name for the operations \(optional\).

**Returns:**

A Queue with the output integers. A `QueueRunner` for the Queue is added to the current `Graph`'s `QUEUE_RUNNER` collection.

### `tf.train.slice_input_producer(tensor_list, num_epochs=None, shuffle=True, seed=None, capacity=32, shared_name=None, name=None)` <a id="slice_input_producer"></a>

Produces a slice of each `Tensor` in `tensor_list`.

Implemented using a Queue -- a `QueueRunner` for the Queue is added to the current `Graph`'s `QUEUE_RUNNER` collection.

**Args:**

* **`tensor_list`**: A list of `Tensor` objects. Every `Tensor` in

   `tensor_list` must have the same size in the first dimension.

* **`num_epochs`**: An integer \(optional\). If specified, `slice_input_producer`

   produces each slice `num_epochs` times before generating

   an `OutOfRange` error. If not specified, `slice_input_producer` can cycle

   through the slices an unlimited number of times.

* **`shuffle`**: Boolean. If true, the integers are randomly shuffled within each

   epoch.

* **`seed`**: An integer \(optional\). Seed used if shuffle == True.
* **`capacity`**: An integer. Sets the queue capacity.
* **`shared_name`**: \(optional\). If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: A name for the operations \(optional\).

**Returns:**

A list of tensors, one for each element of `tensor_list`. If the tensor in `tensor_list` has shape `[N, a, b, .., z]`, then the corresponding output tensor will have shape `[a, b, ..., z]`.

**Raises:**

* **`ValueError`**: if `slice_input_producer` produces nothing from `tensor_list`.

### `tf.train.string_input_producer(string_tensor, num_epochs=None, shuffle=True, seed=None, capacity=32, shared_name=None, name=None)` <a id="string_input_producer"></a>

Output strings \(e.g. filenames\) to a queue for an input pipeline.

**Args:**

* **`string_tensor`**: A 1-D string tensor with the strings to produce.
* **`num_epochs`**: An integer \(optional\). If specified, `string_input_producer`

   produces each string from `string_tensor` `num_epochs` times before

   generating an `OutOfRange` error. If not specified,

   `string_input_producer` can cycle through the strings in `string_tensor`

   an unlimited number of times.

* **`shuffle`**: Boolean. If true, the strings are randomly shuffled within each

   epoch.

* **`seed`**: An integer \(optional\). Seed used if shuffle == True.
* **`capacity`**: An integer. Sets the queue capacity.
* **`shared_name`**: \(optional\). If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: A name for the operations \(optional\).

**Returns:**

A queue with the output strings. A `QueueRunner` for the Queue is added to the current `Graph`'s `QUEUE_RUNNER` collection.

**Raises:**

* **`ValueError`**: If the string\_tensor is a null Python list.  At runtime,

  will fail with an assertion if string\_tensor becomes a null tensor.

### Batching at the end of an input pipeline

These functions add a queue to the graph to assemble a batch of examples, with possible shuffling. They also add a `QueueRunner` for running the subgraph that fills that queue.

Use [`batch`](io_ops.md#batch) or [`batch_join`](io_ops.md#batch_join) for batching examples that have already been well shuffled. Use [`shuffle_batch`](io_ops.md#shuffle_batch) or [`shuffle_batch_join`](io_ops.md#shuffle_batch_join) for examples that would benefit from additional shuffling.

Use [`batch`](io_ops.md#batch) or [`shuffle_batch`](io_ops.md#shuffle_batch) if you want a single thread producing examples to batch, or if you have a single subgraph producing examples but you want to run it in _N_ threads \(where you increase _N_ until it can keep the queue full\). Use [`batch_join`](io_ops.md#batch_join) or [`shuffle_batch_join`](io_ops.md#shuffle_batch_join) if you have _N_ different subgraphs producing examples to batch and you want them run by _N_ threads.

### `tf.train.batch(tensors, batch_size, num_threads=1, capacity=32, enqueue_many=False, shapes=None, dynamic_pad=False, shared_name=None, name=None)` <a id="batch"></a>

Creates batches of tensors in `tensors`.

The argument `tensors` can be a list or a dictionary of tensors. The value returned by the function will be of the same type as `tensors`.

This function is implemented using a queue. A `QueueRunner` for the queue is added to the current `Graph`'s `QUEUE_RUNNER` collection.

If `enqueue_many` is `False`, `tensors` is assumed to represent a single example. An input tensor with shape `[x, y, z]` will be output as a tensor with shape `[batch_size, x, y, z]`.

If `enqueue_many` is `True`, `tensors` is assumed to represent a batch of examples, where the first dimension is indexed by example, and all members of `tensor_list` should have the same size in the first dimension. If an input tensor has shape `[*, x, y, z]`, the output will have shape `[batch_size, x, y, z]`. The `capacity` argument controls the how long the prefetching is allowed to grow the queues.

The returned operation is a dequeue operation and will throw `tf.errors.OutOfRangeError` if the input queue is exhausted. If this operation is feeding another input queue, its queue runner will catch this exception, however, if this operation is used in your main thread you are responsible for catching this yourself.

_N.B.:_ If `dynamic_pad` is `False`, you must ensure that either \(i\) the `shapes` argument is passed, or \(ii\) all of the tensors in `tensors` must have fully-defined shapes. `ValueError` will be raised if neither of these conditions holds.

If `dynamic_pad` is `True`, it is sufficient that the _rank_ of the tensors is known, but individual dimensions may have shape `None`. In this case, for each enqueue the dimensions with value `None` may have a variable length; upon dequeue, the output tensors will be padded on the right to the maximum shape of the tensors in the current minibatch. For numbers, this padding takes value 0. For strings, this padding is the empty string. See `PaddingFIFOQueue` for more info.

**Args:**

* **`tensors`**: The list or dictionary of tensors to enqueue.
* **`batch_size`**: The new batch size pulled from the queue.
* **`num_threads`**: The number of threads enqueuing `tensor_list`.
* **`capacity`**: An integer. The maximum number of elements in the queue.
* **`enqueue_many`**: Whether each tensor in `tensor_list` is a single example.
* **`shapes`**: \(Optional\) The shapes for each example.  Defaults to the

   inferred shapes for `tensor_list`.

* **`dynamic_pad`**: Boolean.  Allow variable dimensions in input shapes.

   The given dimensions are padded upon dequeue so that tensors within a

   batch have the same shapes.

* **`shared_name`**: \(optional\). If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: \(Optional\) A name for the operations.

**Returns:**

A list or dictionary of tensors with the same types as `tensors`.

**Raises:**

* **`ValueError`**: If the `shapes` are not specified, and cannot be

   inferred from the elements of `tensors`.

### `tf.train.batch_join(tensors_list, batch_size, capacity=32, enqueue_many=False, shapes=None, dynamic_pad=False, shared_name=None, name=None)` <a id="batch_join"></a>

Runs a list of tensors to fill a queue to create batches of examples.

The `tensors_list` argument is a list of tuples of tensors, or a list of dictionaries of tensors. Each element in the list is treated similarily to the `tensors` argument of `tf.train.batch()`.

Enqueues a different list of tensors in different threads. Implemented using a queue -- a `QueueRunner` for the queue is added to the current `Graph`'s `QUEUE_RUNNER` collection.

`len(tensors_list)` threads will be started, with thread `i` enqueuing the tensors from `tensors_list[i]`. `tensors_list[i1][j]` must match `tensors_list[i2][j]` in type and shape, except in the first dimension if `enqueue_many` is true.

If `enqueue_many` is `False`, each `tensors_list[i]` is assumed to represent a single example. An input tensor `x` will be output as a tensor with shape `[batch_size] + x.shape`.

If `enqueue_many` is `True`, `tensors_list[i]` is assumed to represent a batch of examples, where the first dimension is indexed by example, and all members of `tensors_list[i]` should have the same size in the first dimension. The slices of any input tensor `x` are treated as examples, and the output tensors will have shape `[batch_size] + x.shape[1:]`.

The `capacity` argument controls the how long the prefetching is allowed to grow the queues.

The returned operation is a dequeue operation and will throw `tf.errors.OutOfRangeError` if the input queue is exhausted. If this operation is feeding another input queue, its queue runner will catch this exception, however, if this operation is used in your main thread you are responsible for catching this yourself.

_N.B.:_ If `dynamic_pad` is `False`, you must ensure that either \(i\) the `shapes` argument is passed, or \(ii\) all of the tensors in `tensors_list` must have fully-defined shapes. `ValueError` will be raised if neither of these conditions holds.

If `dynamic_pad` is `True`, it is sufficient that the _rank_ of the tensors is known, but individual dimensions may have value `None`. In this case, for each enqueue the dimensions with value `None` may have a variable length; upon dequeue, the output tensors will be padded on the right to the maximum shape of the tensors in the current minibatch. For numbers, this padding takes value 0. For strings, this padding is the empty string. See `PaddingFIFOQueue` for more info.

**Args:**

* **`tensors_list`**: A list of tuples or dictionaries of tensors to enqueue.
* **`batch_size`**: An integer. The new batch size pulled from the queue.
* **`capacity`**: An integer. The maximum number of elements in the queue.
* **`enqueue_many`**: Whether each tensor in `tensor_list_list` is a single

   example.

* **`shapes`**: \(Optional\) The shapes for each example.  Defaults to the

   inferred shapes for `tensor_list_list[i]`.

* **`dynamic_pad`**: Boolean.  Allow variable dimensions in input shapes.

   The given dimensions are padded upon dequeue so that tensors within a

   batch have the same shapes.

* **`shared_name`**: \(Optional\) If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: \(Optional\) A name for the operations.

**Returns:**

A list or dictionary of tensors with the same number and types as `tensors_list[i]`.

**Raises:**

* **`ValueError`**: If the `shapes` are not specified, and cannot be

   inferred from the elements of `tensor_list_list`.

### `tf.train.shuffle_batch(tensors, batch_size, capacity, min_after_dequeue, num_threads=1, seed=None, enqueue_many=False, shapes=None, shared_name=None, name=None)` <a id="shuffle_batch"></a>

Creates batches by randomly shuffling tensors.

This function adds the following to the current `Graph`:

* A shuffling queue into which tensors from `tensors` are enqueued.
* A `dequeue_many` operation to create batches from the queue.
* A `QueueRunner` to `QUEUE_RUNNER` collection, to enqueue the tensors

  from `tensors`.

If `enqueue_many` is `False`, `tensors` is assumed to represent a single example. An input tensor with shape `[x, y, z]` will be output as a tensor with shape `[batch_size, x, y, z]`.

If `enqueue_many` is `True`, `tensors` is assumed to represent a batch of examples, where the first dimension is indexed by example, and all members of `tensors` should have the same size in the first dimension. If an input tensor has shape `[*, x, y, z]`, the output will have shape `[batch_size, x, y, z]`.

The `capacity` argument controls the how long the prefetching is allowed to grow the queues.

The returned operation is a dequeue operation and will throw `tf.errors.OutOfRangeError` if the input queue is exhausted. If this operation is feeding another input queue, its queue runner will catch this exception, however, if this operation is used in your main thread you are responsible for catching this yourself.

For example:

```python
# Creates batches of 32 images and 32 labels.
image_batch, label_batch = tf.train.shuffle_batch(
      [single_image, single_label],
      batch_size=32,
      num_threads=4,
      capacity=50000,
      min_after_dequeue=10000)
```

_N.B.:_ You must ensure that either \(i\) the `shapes` argument is passed, or \(ii\) all of the tensors in `tensors` must have fully-defined shapes. `ValueError` will be raised if neither of these conditions holds.

**Args:**

* **`tensors`**: The list or dictionary of tensors to enqueue.
* **`batch_size`**: The new batch size pulled from the queue.
* **`capacity`**: An integer. The maximum number of elements in the queue.
* **`min_after_dequeue`**: Minimum number elements in the queue after a

   dequeue, used to ensure a level of mixing of elements.

* **`num_threads`**: The number of threads enqueuing `tensor_list`.
* **`seed`**: Seed for the random shuffling within the queue.
* **`enqueue_many`**: Whether each tensor in `tensor_list` is a single example.
* **`shapes`**: \(Optional\) The shapes for each example.  Defaults to the

   inferred shapes for `tensor_list`.

* **`shared_name`**: \(Optional\) If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: \(Optional\) A name for the operations.

**Returns:**

A list or dictionary of tensors with the types as `tensors`.

**Raises:**

* **`ValueError`**: If the `shapes` are not specified, and cannot be

   inferred from the elements of `tensors`.

### `tf.train.shuffle_batch_join(tensors_list, batch_size, capacity, min_after_dequeue, seed=None, enqueue_many=False, shapes=None, shared_name=None, name=None)` <a id="shuffle_batch_join"></a>

Create batches by randomly shuffling tensors.

The `tensors_list` argument is a list of tuples of tensors, or a list of dictionaries of tensors. Each element in the list is treated similarily to the `tensors` argument of `tf.train.shuffle_batch()`.

This version enqueues a different list of tensors in different threads. It adds the following to the current `Graph`:

* A shuffling queue into which tensors from `tensors_list` are enqueued.
* A `dequeue_many` operation to create batches from the queue.
* A `QueueRunner` to `QUEUE_RUNNER` collection, to enqueue the tensors

  from `tensors_list`.

`len(tensors_list)` threads will be started, with thread `i` enqueuing the tensors from `tensors_list[i]`. `tensors_list[i1][j]` must match `tensors_list[i2][j]` in type and shape, except in the first dimension if `enqueue_many` is true.

If `enqueue_many` is `False`, each `tensors_list[i]` is assumed to represent a single example. An input tensor with shape `[x, y, z]` will be output as a tensor with shape `[batch_size, x, y, z]`.

If `enqueue_many` is `True`, `tensors_list[i]` is assumed to represent a batch of examples, where the first dimension is indexed by example, and all members of `tensors_list[i]` should have the same size in the first dimension. If an input tensor has shape `[*, x, y, z]`, the output will have shape `[batch_size, x, y, z]`.

The `capacity` argument controls the how long the prefetching is allowed to grow the queues.

The returned operation is a dequeue operation and will throw `tf.errors.OutOfRangeError` if the input queue is exhausted. If this operation is feeding another input queue, its queue runner will catch this exception, however, if this operation is used in your main thread you are responsible for catching this yourself.

**Args:**

* **`tensors_list`**: A list of tuples or dictionaries of tensors to enqueue.
* **`batch_size`**: An integer. The new batch size pulled from the queue.
* **`capacity`**: An integer. The maximum number of elements in the queue.
* **`min_after_dequeue`**: Minimum number elements in the queue after a

   dequeue, used to ensure a level of mixing of elements.

* **`seed`**: Seed for the random shuffling within the queue.
* **`enqueue_many`**: Whether each tensor in `tensor_list_list` is a single

   example.

* **`shapes`**: \(Optional\) The shapes for each example.  Defaults to the

   inferred shapes for `tensors_list[i]`.

* **`shared_name`**: \(optional\). If set, this queue will be shared under the given

   name across multiple sessions.

* **`name`**: \(Optional\) A name for the operations.

**Returns:**

A list or dictionary of tensors with the same number and types as `tensors_list[i]`.

**Raises:**

* **`ValueError`**: If the `shapes` are not specified, and cannot be

   inferred from the elements of `tensors_list`.

