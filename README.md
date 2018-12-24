# Elixir Inconsistencies

The aim of this project is to document all inconsistencies found throughout the Elixir programming
language.
Providing a single page where all inconsistencies can be looked at, hoping that many could be fixed
in next major release, and if not possible users can still be aware of them.
Also a reference to look at when creating new stuff in the Elixir programming language project.

## Convention

### Spelling

- **`Behaviour`**
  - _Affects_: `@behaviour`, `Behaviour` (hard-deprecated in [v1.4]).
  - _Proposed_: `@behavior`, `Behavior`.
  - _Notes_: While all modules, functions, attributes follow the American English spelling,
    this one in particular uses the British English spelling, being borrowed from Erlang.

- **Acronysms**
  Acronysms should be spelled all in uppercase: ie. `pid` should be spelled `PID`.

### Use of underscore

It is a convention to use underscores to separate words, but there are some exceptions:

- **`def*`**
  Functions/macros starting with `def` do not follow this convention:
  - _Affects_: `defdelegate/2`, `defexception/1`, `defimpl/2`, `defimpl/3`, `defmacro/1`, `defmacro/2`, `defmacrop/1`, `defmacrop/2`, `defmodule/2`, `defoverridable/1`, `defp/1`, `defp/2`, `defprotocol/2`, `defstruct/1`.

- **Private functions, macros types**
  `p` suffix meaning private does not use underscore.
  - _Affects_: `defmacrop/1`, `defmacrop/2`, `defp/1`, `defp/2`, `@typep`.
  - _Proposed_:
    - `defmacro_p/1`, `defmacro_p/2`, `def_p/1`, `def_p/2`, `@type_p`, or
    - `defmacro_priv/1`, `defmacro_priv/2`, `def_priv/1`, `def_priv/2`, `@type_priv`.
  - _Notes_: having no underscore and using only one letter (p), makes it difficult sometimes to
    differentiate from the public ones.


## Elixir

### Attributes

- **`behaviour`**
  - _Affects_: `@behaviour`.
  - _Proposed_: `@behavior`.
  - _Notes_: See [Spelling](#spelling) section of this guide for more information.

- **`fallback_to_any`**
  - _Affects_: `@fallback_to_any`.
  - _Proposed_: `@fall_back_on_any`.
  - _Notes_: To "fall back" is a verb and it is two separate words. Fallback is one word when it is a noun.
             Additionally, the phrasal-verb is "to fall back on something", not "to fall back to something"

- **`macrocallback`**
  - _Affects_: `@macrocallback`.
  - _Proposed_: `@macro_callback`.
  - _Presedents_: `@optional_callbacks`.

### Modules and Functions

- **Plural in module names**: names are usually in singular.
  - _Affects_: `Kernel.SpecialForms`, `Kernel.Utils`, `ExUnit.FailuresManifest`, `IO.ANSI.Docs`, `Inspect.Opts`, `List.Chars`,
      `List.Chars.*`, `Stream.Reducers`, `String.Chars`, `String.Chars.*`, `IEx.Helpers`,
      `Mix.Tasks.Compile.Protocols`, `Mix.Tasks.*`, `Mix.Utils`, `:elixir_aliases`,
      `:elixir_clauses`, `:elixir_erl_clauses`, `:elixir_errors`.
  - _Proposed_: `Kernel.SpecialForm`, `Kernel.Util`, `ExUnit.FailureManifest`, `IO.ANSI.Doc`, `Inspect.Opt`, `List.Char`,
      `List.Char.*`, `Stream.Reducer`, `String.Char`, `String.Char.*`, `IEx.Helper`,
      `Mix.Tasks.Compile.Protocol`, `Mix.Task.*`, `Mix.Util`, `:elixir_alias`,
      `:elixir_clause`, `:elixir_erl_clause`, `:elixir_error`.

- **`foldl`**, **`foldr`**
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

- **`macrocallback`**
  - _Affects_: `Behaviour.defmacrocallback/1`.
  - _Proposed_: `Behaviour.defmacro_callback/1`.
  - _Notes_: `Behaviour` module has been hard-deprecated in [v1.4].

- **`opts`**
  - _Affects_: `Inspect.Opts`, `IEx.inspect_opts/0`, `Mix.Tasks.Test.formatter_opts/1`.
  - _Proposed_: `Inspect.Options`, `IEx.inspect_options/0`, `Mix.Tasks.Test.formatter_options/1`.
  - _Proposed alternatively_: `Inspect.Option`.
  - _Precedents_: `OptionParser`, `Kernel.CLI.OptionParsingTest`, `Code.available_compiler_options/0`,
      `Code.compiler_options/0`, `Code.compiler_options/1`, `Mix.SCM.accepts_options/2`.

- **`whereis`**
  - _Affects_: `GenServer.whereis/1`, `Process.whereis/1`.
  - _Proposed_: `GenServer.where_is/1`, `Process.where_is/1`.
  - _Notes_: Borrowed from Erlang's `:erlang.whereis/1`.

- **`IO.bin*`**
  - _Affects_: `IO.binread/2`, `IO.binstream/2`, `IO.binwrite/2`.
  - _Proposed_: `IO.bin_read/2`, `IO.bin_stream/2`, `IO.bin_write/2`.
  - _Proposed alternatively_: `IO.binary_read/2`, `IO.binary_stream/2`, `IO.binary_write/2`.

- **`List.key*`**
  - **`keydelete`**
    - _Affects_: `List.keydelete/3`.
    - _Proposed_: `List.delete_key/3`.
    - _Proposed alternatively_: `List.key_delete/3`, `List.Key.delete/3`.
    - _Precedents_: `Application.delete_env/3`, `Code.delete_path/1`,
      `Keyword.delete_first/2`, `List.delete_at/2`, `Module.delete_attribute/2`, `Process.delete/1`,
      `Supervisor.delete_child/2`, `System.delete_env/1`, `Tuple.delete_at/2`, `Process.get_keys/1`,
      `Dict.has_key?/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keydelete/3`.

  - **`keyfind`**
    - _Affects_: `List.keyfind/4`.
    - _Proposed_: `List.find_key/4`.
    - _Proposed alternatively_: `List.key_find/4`, `List.Key.find/4`.
    - _Precedents_: `Enum.find/3`, `Enum.find_index/2`, `Enum.find_value/3`,
      `System.find_executable/1`, `Task.find/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keyfind/4`.

  - **`keymember?`**
    - _Affects_: `List.keymember?/3`.
    - _Proposed_: `List.member_key?/3` or `List.keymember?/3`.
    - _Proposed alternatively_: `List.Key.member?/3`.
    - _Notes_: name was borrowed from Erlang's `:lists.keymember?/3`.

  - **`keyreplace`**
    - _Affects_: `List.keyreplace/4`.
    - _Proposed_: `List.replace_key/4`.
    - _Proposed alternatively_: `List.key_replace/4` or `List.Key.replace/4`.
    - _Notes_: name was borrowed from Erlang's `:lists.keydelete/3`.

  - **`keysort`**
    - _Affects_: `List.keysort/2`.
    - _Proposed_: `List.sort_key/2`.
    - _Proposed alternatively_: `List.key_sort/2` or `List.Key.sort/2`.
    - _Notes_: name was borrowed from Erlang's `:lists.keysort/3`.

  - **`keystore`**
    - _Affects_: `List.keystore/4`.
    - _Proposed_: `List.store_key/4`.
    - _Proposed_ alternatively: `List.key_store/4` or `List.Key.store/4`.
    - _Notes_: name was borrowed from Erlang's `:lists.keystore/4`.

  - **`keytake`**
    - _Affects_: `List.keytake/3`.
    - _Proposed_: `List.take_key/3`.
    - _Proposed alternatively_: `List.key_take/3` or `List.Key.take/3`.
    - _Notes_: name was borrowed from Erlang's `:lists.keytake/3`.

- **`Path.*name`**
  - _Affects_: all the `Path.*name` functions.
  - _Notes_: I can see this come from Unix/Linux functions,
      but only "basename" and "dirname" are, the rest just come from asimilating the uncommon naming
      convention.

  - **`absname`**
    - _Affects_: `Path.absname/1`, `Path.absname/2`.
    - _Proposed_: `Path.abs_name/1`, `Path.abs_name/2`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands, but there is not such
        `absname` Unix command.

  - **`basename`**
    - _Affects_: `Path.basename/1`, `Path.basename/2`.
    - _Proposed_: `Path.base_name/1`, `Path.base_name/2`.
    - _Notes_: name borrowed from `basename` Unix commands.

  - **`dirname`**
    - _Affects_: `Path.dirname/1`.
    - _Proposed_: `Path.dir_name/1`.
    - _Notes_: name borrowed from `dirname` Unix commands.

  - **`extname`**
    - _Affects_: `Path.extname/1`.
    - _Proposed_: `Path.ext_name/1`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands,
        but there is not such `extname` Unix command.

  - **`rootname`**
    - _Affects_: `Path.rootname/1`.
    - _Proposed_: `Path.root_name/1`.
    - _Notes_: name asimilated from `basename` and `dirname` Unix commands,
        but there is not such `rootname` Unix command.

### Typespecs

- **`ansicode`**
  - _Affects_: `ansicode/0`.
  - _Proposed_: `ansi_code/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

- **`ansidata`**
  - _Affects_: `ansidata/0`.
  - _Proposed_: `ansi_data/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

- **`ansilist`**
  - _Affects_: `ansilist/0`.
  - _Proposed_: `ansi_list/0`.
  - _Presedents_: `IEx.Config.ansi_docs/0`, `:ansi_enabled` option in Elixir application.

- **`iodata`**
  - _Affects_: `iodata/0`.
  - _Proposed_: `io_data/0`.
  - _Presedents_: `File.io_device` and `:std_io` to represent `standard i/o`.

- **`iolist`**
  - _Affects_: `iolist/0`.
  - _Proposed_: `io_list/0`.
  - _Presedents_: `File.io_device` and `:std_io` to represent `standard i/o`.

- **`nodata`**
  - _Affects_: `nodata/0`.
  - _Proposed_: `no_data/0`.
  - _Presedents_: `no_return/0`, `IO.ANSI.no_underline/0`.

- **`non_neg_number`** or **`nonempty_list/0`**
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


## ExUnit

  - DocTest vs doctest
    The module `DocTest` is considered two words (the file is named
      `lib/ex_unit/lib/ex_unit/doc_test.ex`), but the function is named "doctest/2".
    - _Affects_: `ExUnit.DocTest`, `ExUnit.DocTest.doctest`.
    - _Proposed_: `ExUnit.Doctest` and `ExUnit.Doctest.doctest`.
    - _Proposed alternatively_: `ExUnit.DocTest` and `ExUnit.DocTest.doc_test`.


## Mix

### Data

  - Deps status:
    - _Affects_: `:divergedonly`, `:divergedreq`, `:elixirlock`, `:invalidapp`, `:invalidvsn`,
      `:lockmismatch`, `:lockoutdated`, `:noappfile`, `:nolock`, `:nomatchvsn`, `:nosemver`,
      `:scmlock`.
    - _Proposed_: `:diverged_only`, `:diverged_req`, `:elixir_lock`, `:invalid_app`, `:invalid_vsn`,
      `:lock_mismatch`, `:lock_outdated`, `:no_app_file`, `:no_lock`, `:no_match_vsn`, `:no_sem_ver`,
      `:scm_lock`.

### Tasks

  - **`loadconfig`**
    - _Affects_: `mix loadconfig`, `Mix.Tasks.Loadconfig`.
    - _Proposed_: `mix load_config`, `Mix.Tasks.LoadConfig`.

  - **`loadpaths`**
    - _Affects_: `mix loadpaths`, `mix deps.loadpaths`, `Mix.Tasks.Loadpaths`, `Mix.Tasks.Deps.Loadpaths`.
    - _Proposed_: `mix load_paths`, `mix deps.load_paths`, `Mix.Tasks.LoadPaths`, `Mix.Tasks.Deps.LoadPaths`.
    - _Presedents_: `Mix.Projects.load_paths/1`, `mix load_all`, `mix load_tasks`.

[deprecations]: https://hexdocs.pm/elixir/stable/compatibility-and-deprecations.html#table-of-deprecations
[v1.1]: https://github.com/elixir-lang/elixir/blob/v1.1/CHANGELOG.md#4-deprecations
[v1.2]: https://github.com/elixir-lang/elixir/blob/v1.2/CHANGELOG.md#changelog-for-elixir-v12
[v1.3]: https://github.com/elixir-lang/elixir/blob/v1.3/CHANGELOG.md#4-deprecations
[v1.4]: https://github.com/elixir-lang/elixir/blob/v1.4/CHANGELOG.md#4-deprecations
[v1.5]: https://github.com/elixir-lang/elixir/blob/v1.5/CHANGELOG.md#4-deprecations
[v1.6]: https://github.com/elixir-lang/elixir/blob/v1.6/CHANGELOG.md#4-deprecations
[v1.7]: https://github.com/elixir-lang/elixir/blob/v1.7/CHANGELOG.md#4-hard-deprecations

