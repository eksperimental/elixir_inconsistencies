# Elixir Inconsistencies

The aim of this project, is to document all inconsistencies found throughout the Elixir programming
languages.
Providing a single page where all inconsistencies can be looked at, hoping that many could be fixed
in next major release, and if not possible users can still be aware of them.
Also a reference to look at when creating new stuff in the Elixir programming language project.

## Convention

### Use of underscore

It is a convention to use underscores to separate words, but there are some exceptions:

- __`def*`__
  Functions/macros starting with `def` do not follow this convention:
  - _Affects_: `defdelegate/2`, `defexception/1`, `defimpl/2`, `defimpl/3`, `defmacro/1`, `defmacro/2`, `defmacrop/1`, `defmacrop/2`, `defmodule/2`, `defoverridable/1`, `defp/1`, `defp/2`, `defprotocol/2`, `defstruct/1`         

- __Private functions and macros__
  `p` suffix meaning private does not use underscore.
  - _Affects_: `defmacrop/1`, `defmacrop/2`, `defp/1`, `defp/2`, `@typep`
  - _Proposed_:
    - `defmacro_p/1`, `defmacro_p/2`, `def_p/1`, `def_p/2`, `@type_p`, or
    - `defmacro_priv/1`, `defmacro_priv/2`, `def_priv/1`, `def_priv/2`, `@type_priv`.
  - _Notes_: having no underscore and using only one letter (p), makes it difficult sometimes to
    differentiate from the public ones.

## Spelling

- __`Behaviour`__
  - _Affects_: `@behaviour`, `Behaviour` (deprecated).
  - _Proposed_: `@behavior`, `Behavior`.
  - _Notes_: While all modules, functions, attributes follow the American English spelling,
    this one in particular uses the British English spelling, being borrowed from Erlang. 

- _Acronysms__
  Acronysms should be spelled all in uppercase such as: `pid`. 

## Considerations



## Elixir

### Functions

- __`whereis`__
  - _Affects_: `GenServer.whereis/1`, `Process.whereis/1`.
  - _Proposed_: `GenServer.where_is/1`, `Process.where_is/1`.
  - _Notes_: Borrowed from Erlang's `:erlang.whereis/1`.
  
- __`foldl`__, __`foldr`__
  - _Affects_: `List.foldl/3`, `List.foldr/3`.
  - _Proposed_:
    - `List.fold_left/3` and `List.fold_right/3`, or
    - `List.fold_l/3` and`List.fold_r/3`.
  - _Notes_: These List.fold* functions come from Haskell, but it is weird to have l & r as
      left and right, as they are not seen in it in other function names.
    Other functions use a single letter, but these are Unix command, and they refer to the short
      version of the argument, such as `File.cp_r/3`, `File.rm_rf/1`, `File.ln_s/2`.
    So I propose we use "_left" and "_right" to be more explicit,
    and to make a clear difference away from single letters that represent short arguments.

- __`macrocallback`__
  - _Affects_: `Behaviour.defmacrocallback/1`.
  - _Proposed_: `Behaviour.defmacro_callback/1`.
  - _Notes_: `Behaviour` module has been deprecated.

- __`List.key*`__
  - __`keydelete`__
    - _Affects_: `List.keydelete/3`.
    - _Proposed_: `List.delete_key/3`, `List.Key.delete/3`.
    - _Precedents_: `Application.delete_env/3`, `Code.delete_path/1`,
      `Keyword.delete_first/2`, `List.delete_at/2`, `Module.delete_attribute/2`, `Process.delete/1`,
      `Supervisor.delete_child/2`, `System.delete_env/1`, `Tuple.delete_at/2`, `Process.get_keys/1`,
      `Dict.has_key?/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keydelete/3`.

  - __`keyfind`__
    - _Affects_: `List.keyfind/4`.
    - _Proposed_: `List.find_key/4`, `List.Key.find/4`.
    - _Precedents_: `Enum.find/3`, `Enum.find_index/2`, `Enum.find_value/3`,
      `System.find_executable/1`, `Task.find/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keyfind/4`.

  - __`keymember?`__
    - _Affects_: `List.keymember?/3`.
    - _Proposed_: `List.member_key?/3` or `List.Key.member?/3`.
    - _Notes_: name was borrowed from Erlang's `:lists.keymember?/3`.

  - __`keyreplace`__
    - _Affects_: `List.keyreplace/4`.
    - _Proposed_: `List.replace_key/4` or `List.Key.replace/4`.
    - _Notes_: name was borrowed from Erlang's `:lists.keydelete/3`.

  - __`keyreplace`_
    - Affects: `List.keyreplace/4`.
    - Proposed: `List.replace_key/4` or `List.Key.replace/4`.
    - Notes: name was borrowed from Erlang's `:lists.keyreplace/3`.

  - __`keysort`__
    - _Affects_: `List.keysort/2`.
    - _Proposed_: `List.sort_key/2` or `List.Key.sort/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keysort/3`.

  - __`keystore`__
    - _Affects_: `List.keystore/4`.
    - _Proposed_: `List.store_key/4` or `List.Key.store/4`.
    - _Notes_: name was borrowed from Erlang's `:lists.keystore/4`.

  - __`keytake`__
    - _Affects_: `List.keytake/3`.
    - _Proposed_: `List.take_key/3` or `List.Key.take/3`.
    - _Notes_: name was borrowed from Erlang's `:lists.keytake/3`.

- __`Path.*name`__
  - _Affects_: all the `Path.*name` functions. I can see this come from Unix/Linux functions,
    but only "basename" and "dirname" are, the rest just come from asimilating the uncommon naming
    convention.

  - __`absname`__
    - _Affects_: `Path.absname/1`, `Path.absname/2`.
    - _Proposed_: `Path.abs_name/1`, `Path.abs_name/2`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands, but there is not such
      `absname` Unix command.

  - __`basename`__
    - _Affects_: `Path.basename/1`, `Path.basename/2`.
    - _Proposed_: `Path.base_name/1`, `Path.base_name/2`.
    - _Notes_: name borrowed from `basename` Unix commands.

  - __`dirname`__
    - _Affects_: `Path.dirname/1`.
    - _Proposed_: `Path.dir_name/1`.
    - _Notes_: name borrowed from `dirname` Unix commands.
- 
  - __`extname`__
    - _Affects_: `Path.extname/1`.
    - _Proposed_: `Path.ext_name/1`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands,
      but there is not such `extname` Unix command.

  - __`rootname`__
    - _Affects_: `Path.rootname/1`.
    - _Proposed_: `Path.root_name/1`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands,
      but there is not such `rootname` Unix command.

### Typespecs

- __`non_neg_number`__ or __`nonempty_list/0`__
  - _Affects_: `non_neg_number/0`, `non_empty_list/0`.
  - _Proposed_:
    - `nonneg_number/0` and `nonempty_list/0`, or
    - `non_neg_number/0` and `non_empty_list/0`.
  - _Notes_: "non" is a prefix, that can be used along with hyphen as in non-negative, or without it
    as in nonnegative.
    [most of the words in English](https://en.wiktionary.org/wiki/Category:English_words_prefixed_with_non-)
    use it without a hyphen, but both, non-empty and non-negative are found.
    My proposal is to stick to one convention for all prefixes using "non",
    preferably using the hyphen/underscore to avoid having things like "nonneg_number".
  - References: [non-empty](https://en.wiktionary.org/wiki/non-empty) and
    [non-negative](https://en.wiktionary.org/wiki/non-negative) entries in Wikitionary.

- __`iodata`__
  - _Affects_: `iodata/0`.
  - _Proposed_: `io_data/0`.
  - _Presedents_: `File.io_device` and `:std_io` to represent `standard i/o`/.

- __`iolist`__
  - _Affects_: `iolist/0`.
  - _Proposed_: `io_list/0`.
  - _Presedents_: `File.io_device` and `:std_io` to represent `standard i/o`/.

- __`nodata`__
  - _Affects_: `nodata/0`.
  - _Proposed_: `no_data/0`.
  - _Presedents_: `no_return/0`, `IO.ANSI.no_underline/0`.

- __`ansidata`__
  - _Affects_: `ansidata/0`.
  - _Proposed_: `ansi_data/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

- __`ansilist`__
  - _Affects_: `ansilist/0`.
  - _Proposed_: `ansi_list/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

- __`ansicode`__
  - _Affects_: `ansicode/0`.
  - _Proposed_: `ansi_code/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

### Attributes

- __`macrocallback`__
  - _Affects_: `@macrocallback`.
  - _Proposed_: `@macro_callback`.
  - _Presedents_: `@optional_callbacks`.

- __`behaviour`__
  - _Affects_: `@behaviour`.
  - _Proposed_: `@behavior`.
  - _Notes_: See [Spelling](#spelling) section of this guide for more information.


## Mix

### Tasks

  - __`loadconfig`__
    - _Affects_: `mix loadconfig`, `Mix.Tasks.Loadconfig`.
    - _Proposed_: `mix load_config`, `Mix.Tasks.LoadConfig`.
