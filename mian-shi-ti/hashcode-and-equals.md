# hashcode & equals

```java
/**
 * Returns a hash code value for the object. This method is
 * supported for the benefit of hash tables such as those provided by
 * {@link java.util.HashMap}.
 */
@HotSpotIntrinsicCandidate
public native int hashCode();

/**
 * Note that it is generally necessary to override the {@code hashCode}
 * method whenever this method is overridden, so as to maintain the
 * general contract for the {@code hashCode} method, which states
 * that equal objects must have equal hash codes.
 */
public boolean equals(Object obj) {
    return (this == obj);
}
```

