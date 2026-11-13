# adhoc_command___cached_with_auto_inputs_and_outputs

`vt run --cache -- <command>` runs a command that no task defines, cached like a script: inputs and outputs are tracked automatically.

## `vt run --cache -- vtt fs read src/input.txt write output.txt built`

first run — cache miss

```
$ vtt fs read src/input.txt write output.txt built
```

## `vtt rm output.txt`

delete the output to prove the restore is real

```
```

## `vt run --cache -- vtt fs read src/input.txt write output.txt built`

second run — cache hit, restores the output

```
$ vtt fs read src/input.txt write output.txt built ◉ cache hit, replaying

---
vt run: cache hit.
```

## `vtt print-file output.txt`

output restored from the cache

```
built
```

## `vtt replace-file-content src/input.txt initial modified`

```
```

## `vt run --cache -- vtt fs read src/input.txt write output.txt built`

cache miss: the input changed

```
$ vtt fs read src/input.txt write output.txt built ○ cache miss: 'src/input.txt' modified, executing
```

## `vt run -- vtt fs read src/input.txt write output.txt built`

without `--cache`, an ad-hoc command is uncached, like a script

```
$ vtt fs read src/input.txt write output.txt built ⊘ cache disabled
```
