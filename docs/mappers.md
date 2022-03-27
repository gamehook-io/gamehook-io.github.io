---
title: Mappers
layout: subpage
---

These mappers are designed to provide a memory layout that then map to objects when loaded into GameHook.

## File top-level fields
`meta`

`macros` (optional)

`properties`

`glossary`


## Property Types
### **string**
This translates the property into a human-readable string.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`reference` | No | defaultCharacterMap | Which glossary item provides the mapping.
`note` | No | | Note section

### **int**
This translates the property into a number (int32).

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **uint**
This translates the property into a unsigned number (uint32).

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **binaryCodedDecimal**
This translates the property into a number which is binary encoded (where each digit in a decimal number is represented in the form of bits)

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **bool**
This returns the property as a true / false value.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **bit**
This returns the property as a single bit.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **bitArray**
This returns the property as a array of bits.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`note` | No | | Note section

### **reference**
This looks up the property's value by it's key in a glossary item.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`length` | No | 1 | How many bytes until the ending address
`reference` | Yes |  | Which glossary item provides the mapping.
`note` | No | | Note section

### **macro**
This allows you to define macros / structures of reusable data. This property will automatically be replaced with the macro defined.

| Argument | Required | Default Value | Description |
`startingAddress` | Yes | | The starting address for the property.
`macro` | Yes |  | Which macro provides the values for this property.
`note` | No | | Note section

## Macro Properties
Macros can be used to create reusable property groups. \
These are still properties, so please see above for the correct layout.

| Argument | Required | Default Value | Description |
`offset` | Yes |  | The offset from the starting address.
`type` | Yes | | The type this property represents.