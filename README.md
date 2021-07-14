
# `sesterl_testing`: A Unit Testing Library for Sesterl Programs

## How to use

1. Add the dependency on this library to `sesterl.yaml` in your project:

   ```yaml
   test_dependencies:
     - name: "sesterl_testing"
       source:
         type: "git"
         repository: "https://github.com/gfngfn/sesterl_testing"
         spec:
           type: "branch"
           value: "master"
   ```

2. Generate `rebar.config` from `sesterl.yaml`:

   ```console
   $ sesterl config ./
   ```

3. Write unit tests (see the next section for detail).

4. Run them:

   ```console
   $ rebar3 sesterl test
   ```


## How to write unit tests

Consider testing the following module `Mod` for instance:

```
/* -- src/Mod.sest -- */
module Mod = struct

  val add(m, n) = m + n

end
```

You can write unit tests for `Mod` by providing the following module:

```
/* -- test/ModTests.sest -- */
import Mod

module ModTests = #[test] struct

  #[test]
  val add_test() =
    Testing.it("integer addition", fun() ->
      assert Testing.equal(
        -expect 99,
        -got    Mod.add(42, 57),
      )
    end)

end
```
