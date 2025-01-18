# `aiida-quantumespresso`
[![PyPI version](https://badge.fury.io/py/aiida-quantumespresso.svg)](https://badge.fury.io/py/aiida-quantumespresso)
[![PyPI pyversions](https://img.shields.io/pypi/pyversions/aiida-quantumespresso.svg)](https://pypi.python.org/pypi/aiida-quantumespresso)
[![Build Status](https://github.com/aiidateam/aiida-quantumespresso/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/aiidateam/aiida-quantumespresso/actions)
[![Docs status](https://readthedocs.org/projects/aiida-quantumespresso/badge)](http://aiida-quantumespresso.readthedocs.io/)

This is the official AiiDA plugin for [Quantum ESPRESSO](https://www.quantum-espresso.org/).

## Compatibility matrix

The matrix below assumes the user always install the latest patch release of the specified minor version, which is recommended.

| Plugin | AiiDA | Python | Quantum ESPRESSO |
|-|-|-|-|
| `v4.8 < v5.0` | ![Compatibility for v4.0][AiiDA v4.0] |  [![PyPI pyversions](https://img.shields.io/pypi/pyversions/aiida-quantumespresso.svg)](https://pypi.org/project/aiida-quantumespresso) | ![Quantum ESPRESSO compatibility][QE v6.6-7.4] |
| `v4.3 < v4.8` | ![Compatibility for v4.0][AiiDA v4.0] |  [![PyPI pyversions](https://img.shields.io/pypi/pyversions/aiida-quantumespresso.svg)](https://pypi.org/project/aiida-quantumespresso) | ![Quantum ESPRESSO compatibility][QE v6.6-7.3] |
| `v4.0 < v4.3` | ![Compatibility for v4.0][AiiDA v4.0] |  [![PyPI pyversions](https://img.shields.io/pypi/pyversions/aiida-quantumespresso.svg)](https://pypi.org/project/aiida-quantumespresso) | ![Quantum ESPRESSO compatibility][QE v6.6-7.1] |
| `v3.5 < v4.0` | ![Compatibility for v3.5][AiiDA v3.5] |  [![PyPI pyversions][Python v3.6-v3.9]](https://pypi.org/project/aiida-quantumespresso/3.5.2/) | ![Quantum ESPRESSO compatibility][QE v6-7] |
| `v3.4 < v3.5` | ![Compatibility for v3.4][AiiDA v3.4] |  [![PyPI pyversions][Python v3.6-v3.9]](https://pypi.org/project/aiida-quantumespresso/3.4.2/) | ![Quantum ESPRESSO compatibility][QE v6] |
| `v3.3 < v3.4` | ![Compatibility for v3.3][AiiDA v3.3] |  [![PyPI pyversions][Python v3.6-v3.8]](https://pypi.org/project/aiida-quantumespresso/3.3.1/) | ![Quantum ESPRESSO compatibility][QE v6] |
| `v3.1 < v3.3` | ![Compatibility for v3.1][AiiDA v3.1] |  [![PyPI pyversions][Python v3.5-v3.8]](https://pypi.org/project/aiida-quantumespresso/3.2.1/) | ![Quantum ESPRESSO compatibility][QE v6] |
| `v3.0 < v3.1` | ![Compatibility for v3.0][AiiDA v3.0] |  [![PyPI pyversions][Python v2.7-v3.8]](https://pypi.org/project/aiida-quantumespresso/3.0.0/) | ![Quantum ESPRESSO compatibility][QE v6] |
| `v2.0 < v3.0` | ![Compatibility for v2.0][AiiDA v2.0] |  [![PyPI pyversions][Python v2.7-v3.8]](https://pypi.org/project/aiida-quantumespresso/2.1.0/) | ![Quantum ESPRESSO compatibility][QE v6] |

Starting from `aiida-quantumespresso==4.0`, the last three minor versions of Quantum ESPRESSO are supported.
Older versions are supported up to a maximum of two years.

## Installation
To install from PyPI, simply execute:

    pip install aiida-quantumespresso

or when installing from source:

    git clone https://github.com/aiidateam/aiida-quantumespresso
    pip install aiida-quantumespresso

## Command line interface tool
The plugin comes with a builtin CLI tool: `aiida-quantumespresso`.
This tool is built using the `click` library and supports tab-completion.
To enable it, add the following to your shell loading script, e.g. the `.bashrc` or virtual environment activate script:

    eval "$(_AIIDA_QUANTUMESPRESSO_COMPLETE=source aiida-quantumespresso)"

The tool comes with various sub commands, for example to quickly launch some calculations and workchains
For example, to launch a test `PwCalculation` you can run the following command:

    aiida-quantumespresso calculation launch pw -X pw-v6.1 -F SSSP/1.1/PBE/efficiency

Note that this requires the code `pw-v6.1` and pseudopotential family `SSSP/1.1/PBE/efficiency` to be configured.
See the pseudopotentials section on how to install them easily.
Each command has a fully documented command line interface, which can be printed to screen with the help flag:

    aiida-quantumespresso calculation launch ph --help

which should print something like the following:

    Usage: aiida-quantumespresso calculation launch ph [OPTIONS]

      Run a PhCalculation.

    Options:
      -X, --code CODE                 A single code identified by its ID, UUID or
                                      label.  [required]
      -C, --calculation CALCULATION   A single calculation identified by its ID or
                                      UUID.  [required]
      -k, --kpoints-mesh INTEGER...   The number of points in the kpoint mesh
                                      along each basis vector.  [default: 1, 1, 1]
      -m, --max-num-machines INTEGER  The maximum number of machines (nodes) to
                                      use for the calculations.  [default: 1]
      -w, --max-wallclock-seconds INTEGER
                                      the maximum wallclock time in seconds to set
                                      for the calculations.  [default: 1800]
      -i, --with-mpi                  Run the calculations with MPI enabled.
                                      [default: False]
      -d, --daemon                    Submit the process to the daemon instead of
                                      running it locally.  [default: False]
      -h, --help                      Show this message and exit.

## Pseudopotentials
Pseudopotentials are installed and managed through the [`aiida-pseudo` plugin](https://pypi.org/project/aiida-pseudo/).
The easiest way to install pseudopotentials, is to install a version of the [SSSP](https://www.materialscloud.org/discover/sssp/table/efficiency) through the CLI of `aiida-pseudo`.
Simply run

    aiida-pseudo install sssp

to install the default SSSP version.
List the installed pseudopotential families with the command `aiida-pseudo list`.
You can then use the name of any family in the command line using the `-F` flag.

## Development

### Running tests
To run the tests, simply clone and install the package locally with the [tests] optional dependencies:

```shell
git clone https://github.com/aiidateam/aiida-quantumespresso .
cd aiida-quantumespresso
pip install -e .[tests]  # install extra dependencies for test
pytest # run tests
```

You can also use `tox` to run the test set. Here you can also use the `-e` option to specify the Python version for the test run:
```shell
pip install tox
tox -e py39 -- tests/calculations/test_pw.py
```

### Pre-commit
To contribute to this repository, please enable pre-commit so the code in commits are conform to the standards.
Simply install the repository with the `pre-commit` extra dependencies:
```shell
cd aiida-quantumespresso
pip install -e .[pre-commit]
pre-commit install
```

## License
The `aiida-quantumespresso` plugin package is released under the MIT license.
See the `LICENSE.txt` file for more details.

## Acknowledgements
We acknowledge support from:
* the [NCCR MARVEL](http://nccr-marvel.ch/) funded by the Swiss National Science Foundation;
* the EU Centre of Excellence "[MaX – Materials Design at the Exascale](http://www.max-centre.eu/)" (Horizon 2020 EINFRA-5, Grant No. 676598; H2020-INFRAEDI-2018-1, Grant No. 824143; HORIZON-EUROHPC-JU-2021-COE-1, Grant No. 101093374);
* the European Union's Horizon 2020 research and innovation programme (Grant No. 957189, [project BIG-MAP](https://www.big-map.eu), also part of the [BATTERY 2030+ initiative](https://battery2030.eu), Grant No. 957213);
* the [swissuniversities P-5 project "Materials Cloud"](https://www.materialscloud.org/swissuniversities).

<img src="https://raw.githubusercontent.com/aiidateam/aiida-quantumespresso/develop/docs/source/images/MARVEL.png" width="250px" height="131px"/>
<img src="https://raw.githubusercontent.com/aiidateam/aiida-quantumespresso/develop/docs/source/images/MaX.png" width="300px" height="84px"/>
<img src="https://raw.githubusercontent.com/aiidateam/aiida-quantumespresso/develop/docs/source/images/BIG-MAP_logo.png" width="77px" height="107px"/>
<img src="https://raw.githubusercontent.com/aiidateam/aiida-quantumespresso/develop/docs/source/images/swissuniversities.png" width="300px" height="35px"/>

[AiiDA v4.0]: https://img.shields.io/badge/AiiDA->=2.0.0,<3.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v3.5]: https://img.shields.io/badge/AiiDA->=1.4.4,<2.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v3.4]: https://img.shields.io/badge/AiiDA->=1.4.4,<2.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v3.3]: https://img.shields.io/badge/AiiDA->=1.4.4,<2.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v3.1]: https://img.shields.io/badge/AiiDA->=1.2.0,<2.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v3.0]: https://img.shields.io/badge/AiiDA->=1.0.0,<1.1.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D
[AiiDA v2.0]: https://img.shields.io/badge/AiiDA->=0.12,<1.0.0-007ec6.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAhCAYAAABTERJSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAFhgAABYYBG6Yz4AAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAUbSURBVFiFzZhrbFRVEMd%2Fc%2B5uu6UUbIFC%2FUAUVEQCLbQJBIiBDyiImJiIhmohYNCkqJAQxASLF8tDgYRHBLXRhIcKNtFEhVDgAxBJqgmVh4JEKg3EIn2QYqBlt917xg%2BFss%2ByaDHOtzsz5z%2B%2FuZl7ztmF%2F5HJvxVQN6cPYX8%2FPLnOmsvNAvqfwuib%2FbNIk9cQeQnLcKRL5xLIV%2Fic9eJeunjPYbRs4FjQSpTB3aS1IpRKeeOOewajy%2FKKEO8Q0DuVdKy8IqsbPulxGHUfCBBu%2BwUYGuFuBTK7wQnht6PEbf4tlRomVRjCbXNjQEB0AyrFQOL5ENIJm7dTLZE6DPJCnEtFZVXDLny%2B4Sjv0PmmYu1ZdUek9RiMgoDmJ8V0L7XJqsZ3UW8YsBOwEeHeeFce7jEYXBy0m9m4BbXqSj2%2Bxnkg26MCVrN6DEZcwggtd8pTFx%2Fh3B9B50YLaFOPwXQKUt0tBLegtSomfBlfY13PwijbEnhztGzgJsK5h9W9qeWwBqjvyhB2iBs1Qz0AU974DciRGO8CVN8AJhAeMAdA3KbrKEtvxhsI%2B9emWiJlGBEU680Cfk%2BSsVqXZvcFYGXjF8ABVJ%2BTNfVXehyms1zzn1gmIOxLEB6E31%2FWBe5rnCarmo7elf7dJEeaLh80GasliI5F6Q9cAz1GY1OJVNDxTzQTw7iY%2FHEZRQY7xqJ9RU2LFe%2FYqakdP911ha0XhjjiTVAkDwgatWfCGeYocx8M3glG8g8EXhSrLrHnEFJ5Ymow%2FkhIYv6ttYUW1iFmEqqxdVoUs9FmsDYSqmtmJh3Cl1%2BVtl2s7owDUdocR5bceiyoSivGTT5vzpbzL1uoBpmcAAQgW7ArnKD9ng9rc%2BNgrobSNwpSkkhcRN%2BvmXLjIsDovYHHEfmsYFygPAnIDEQrQPzJYCOaLHLUfIt7Oq0LJn9fxkSgNCb1qEIQ5UKgT%2Fs6gJmVOOroJhQBXVqw118QtWLdyUxEP45sUpSzqP7RDdFYMyB9UReMiF1MzPwoUqHt8hjGFFeP5wZAbZ%2F0%2BcAtAAcji6LeSq%2FMYiAvSsdw3GtrfVSVFUBbIhwRWYR7yOcr%2FBi%2FB1MSJZ16JlgH1AGM3EO2QnmMyrSbTSiACgFBv4yCUapZkt9qwWVL7aeOyHvArJjm8%2Fz9BhdI4XcZgz2%2FvRALosjsk1ODOyMcJn9%2FYI6IrkS5vxMGdUwou2YKfyVqJpn5t9aNs3gbQMbdbkxnGdsr4bTHm2AxWo9yNZK4PXR3uzhAh%2BM0AZejnCrGdy0UvJxl0oMKgWSLR%2B1LH2aE9ViejiFs%2BXn6bTjng3MlIhJ1I1TkuLdg6OcAbD7Xx%2Bc3y9TrWAiSHqVkbZ2v9ilCo6s4AjwZCzFyD9mOL305nV9aonvsQeT2L0gVk4OwOJqXXVRW7naaxswDKVdlYLyMXAnntteYmws2xcVVZzq%2BtHPAooQggmJkc6TLSusOiL4RKgwzzYU1iFQgiUBA1H7E8yPau%2BZl9P7AblVNebtHqTgxLfRqrNvZWjsHZFuqMqKcDWdlFjF7UGvX8Jn24DyEAykJwNcdg0OvJ4p5pQ9tV6SMlP4A0PNh8aYze1ArROyUNTNouy8tNF3Rt0CSXb6bRFl4%2FIfQzNMjaE9WwpYOWQnOdEF%2BTdJNO0iFh7%2BI0kfORzQZb6P2kymS9oTxzBiM9rUqLWr1WE5G6ODhycQd%2FUnNVeMbcH68hYkGycNoUNWc8fxaxfwhDbHpfwM5oeTY7rUX8QAAAABJRU5ErkJggg%3D%3D

[Python v3.6-v3.9]: https://img.shields.io/badge/python-3.6%20%7C%203.7%20%7C%203.8%20%7C%203.9-blue
[Python v3.6-v3.8]: https://img.shields.io/badge/python-3.6%20%7C%203.7%20%7C%203.8-blue
[Python v3.5-v3.8]: https://img.shields.io/badge/python-3.5%20%7C%203.6%20%7C%203.7%20%7C%203.8-blue
[Python v2.7-v3.8]: https://img.shields.io/badge/python-2.7%20%7C%203.5%20%7C%203.6%20%7C%203.7%20%7C%203.8-blue

[QE v6]: https://img.shields.io/badge/Quantum%20ESPRESSO->=6.0,<=6.7-007ec6.svg?logo=data:image/png;base64,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
[QE v6-7]: https://img.shields.io/badge/Quantum%20ESPRESSO->=6.0,<=7.0-007ec6.svg?logo=data:image/png;base64,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
[QE v6.6-7.1]: https://img.shields.io/badge/Quantum%20ESPRESSO->=6.6,<=7.1-007ec6.svg?logo=data:image/png;base64,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
[QE v6.6-7.3]: https://img.shields.io/badge/Quantum%20ESPRESSO->=6.6,<=7.3-007ec6.svg?logo=data:image/png;base64,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
[QE v6.6-7.4]: https://img.shields.io/badge/Quantum%20ESPRESSO->=6.6,<=7.4-007ec6.svg?logo=data:image/png;base64,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
