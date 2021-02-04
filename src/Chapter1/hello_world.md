
Let's begin with a classical program in Computer Science - Hello World, to help you better understand ACPI:

```asl
DefinitionBlock ("", "DSDT", 2, "", "", 0x0)
{
	Method (MTH1) {
		printf("Hello World")
	}
}
```

In the basic structure `DefinitionBlock`, we defined a method named `MTH1`, which can be called to print the "Hello World" string.

We will go further on the terms in the other chapters. So, keep calm and continue, just like the first lesson that you have done with the other programming languages.

To compile it, type:

```
iasl hello_world.asl
```

Without error, you should see a `hello_world.aml` and the following output:

    ASL Input:     hello_world.asl -      93 bytes      1 keywords      8 source lines
    AML Output:    hello_world.aml -      59 bytes      0 opcodes       1 named objects

    Compilation successful. 0 Errors, 0 Warnings, 0 Remarks, 0 Optimizations

ACPIAC also provides an utility, `acpiexec` as an emulated ACPI execution environment.
We can use it to test our compiled `aml` file.

```
acpiexec hello_world.aml
```

The file will be loaded by the emulator, and it waits for our operation after initialization:

    Input file hello_world.aml, Length 0x3B (59) bytes

    ACPI: RSDP 0x000055947CC940A0 000024 (v02 Intel )
    ACPI: XSDT 0x000055947E0B1D20 000034 (v00 Intel  AcpiExec 00001001 INTL 20210105)
    ACPI: FACP 0x000055947CC93EC0 000114 (v05 Intel  AcpiExec 00001001 INTL 20210105)
    ACPI: DSDT 0x000055947E0B74F0 00003B (v02                 00000000 INTL 20210105)
    ACPI: FACS 0x000055947CC94060 000040


    ACPI table initialization:
    Table [DSDT:         ] (id 01) -    1 Objects with   0 Devices,   0 Regions,    1 Methods (0/1/0 Serial/Non/Cvt)
    ACPI: 1 ACPI AML tables successfully acquired and loaded

    Final data object initialization: Namespace contains 10 (0xA) objects
    Initializing General Purpose Events (GPEs):
        Initialized GPE 00 to 7F [_GPE] 16 regs on interrupt 0x0 (SCI)
        Initialized GPE 80 to FF [_GPE] 16 regs on interrupt 0x0 (SCI)
    Initializing Device/Processor/Thermal objects and executing _INI/_STA methods:
        Executed 0 _INI methods requiring 0 _STA executions (examined 2 objects)
    - 

We aim at running the `MTH1` method and seeing the **Hello World** output. We need to **evaluate**/**execute** the method.
To do so, type `Execute \MTH1`, where `Execute` is a command in `acpiexec`, `MTH1` is a the method name under `\` (root, DOS-style).

We can then see the debug output `"Hello World"` surrounded by some prompts:

    Evaluating \MTH1
    ACPI Debug:  "Hello World"
    No object was returned from evaluation of \MTH1

We will dig more details of `acpiexec` in the following chapters.

If you reach here, it means you have started your first step to fully understand ACPI. Keep reading :)
