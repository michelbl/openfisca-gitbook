# Tests

OpenFisca has three sorts of tests:

* unit tests
* test-case tests
* scenario tests

## Run tests

OpenFisca uses [nose](https://nose.readthedocs.org/) to run its unit tests. Here are some useful commands.

- Run the whole test suite:
    ```
    make test
    ```
    which is available at least in Core, France and Web-API repositories.
- Run a specific test:
    ```
    nosetests openfisca_france/tests/test_legislations.py
    ```
- Hide log of failing test:
    ```
    nosetests --nologcapture openfisca_france/tests/test_legislations.py
    ```
- Display log of successful test:
    ```
    nosetests --debug=openfisca_core openfisca_france/tests/test_legislations.py
    ```

## YAML tests

Formulas are tested with [YAML tests](../coding-the-legislation/writing_yaml_tests.md).


## ipdb debugger

If a test fails, you can execute it with the [debug](https://nose.readthedocs.org/en/latest/plugins/debug.html) nose plugin:

```bash
nosetests --pdb openfisca_core/tests/test_tax_scales.py
```

You'll be dropped in the `pdf` debugger shell when an error occurs.

You can [specify the exact test to launch](https://nose.readthedocs.org/en/latest/usage.html#selecting-tests):

```bash
nosetests --pdb openfisca_core/tests/test_tax_scales.py:test_linear_average_rate_tax_scale
```

> The [nose-ipdb](https://github.com/flavioamieiro/nose-ipdb/) plugin is more user-friendly
> (because it uses the [ipdb](https://github.com/gotcha/ipdb) debugger instead of pdb).
> In this case, just use the `--ipdb` option rather than `--pdb`.
> See also the `--ipdb-failure` option.

In case you want to set a breakpoint manually, in order to enter the debugger shell before an errors occurs,
copy-paste this line in your code:

```python
import nose.tools; nose.tools.set_trace(); import ipdb; ipdb.set_trace()
```

This needs [ipdb](https://github.com/gotcha/ipdb) to be installed.

> Hint: use the snippets feature of your favorite text editor to save this line, for example give it the name "breakpoint".

## Travis automated tests

OpenFisca uses [Travis CI](https://travis-ci.org/openfisca) to run tests automatically after each `git push`.

The repositories tested by Travis are:

* [OpenFisca-Core](https://github.com/openfisca/openfisca-core)
* [OpenFisca-France](https://github.com/openfisca/openfisca-france)
* [OpenFisca-Web-API](https://github.com/openfisca/openfisca-web-api)

The OpenFisca website hosts a summary page of the build statuses: https://www.openfisca.fr/build-status

Travis tests other git branches than `master` too. For example: [OpenFisca-Core](https://travis-ci.org/openfisca/openfisca-core/branches).

For OpenFisca-France, when testing a branch, if there is a branch in OpenFisca-Core with the same name, Travis will checkout it before running the tests. This is done by [this script](https://github.com/openfisca/openfisca-france/blob/master/run-travis-tests.sh).

Idem for OpenFisca-Web-API with [this script](https://github.com/openfisca/openfisca-web-api/blob/master/run-travis-tests.sh) which is sightly different because it handles more dependencies.

## Ludwig tests

To download tests from [Ludwig](https://mes-aides.gouv.fr/tests/) (the tests tool from [Mes aides](https://mes-aides.gouv.fr/)), see the script [download_mes_aides_tests.py](https://github.com/openfisca/openfisca-france/blob/master/openfisca_france/scripts/download_mes_aides_tests.py).
