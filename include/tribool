///////////////////////////////////////////////////////////////////////////////
//
// Copyright (C) 2013 Bjorn Reese <breese@users.sourceforge.net>
//
// Permission to use, copy, modify, and distribute this software for any
// purpose with or without fee is hereby granted, provided that the above
// copyright notice and this permission notice appear in all copies.
//
// THIS SOFTWARE IS PROVIDED ``AS IS'' AND WITHOUT ANY EXPRESS OR IMPLIED
// WARRANTIES, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF
// MERCHANTIBILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE AUTHORS AND
// CONTRIBUTORS ACCEPT NO RESPONSIBILITY IN ANY CONCEIVABLE MANNER.
//
///////////////////////////////////////////////////////////////////////////////

namespace xstd
{

struct basic_tribool_kleene_tag {};
struct basic_tribool_neutral_tag {};

template <typename Type>
struct basic_tribool_traits
{
    // Specializations must implement
    //  negation
    //  conjunction
    //  disjunction
};

template <typename Type>
class basic_tribool
{
public:
    typedef basic_tribool_traits<Type> traits_type;

    basic_tribool()
        : value(traits_type::indeterminate_value)
    {}

    basic_tribool(bool initial_value)
    : value(initial_value
            ? traits_type::true_value
            : traits_type::false_value)
    {}

    basic_tribool(typename traits_type::value_type value)
        : value(value)
    {}

    operator bool() const { return value == traits_type::true_value; }

    inline basic_tribool<Type> operator ! ()
    {
        return traits_type::negation(value);
    }

    inline basic_tribool<Type> operator && (basic_tribool<Type> other)
    {
        return traits_type::conjunction(value, other.value);
    }

    inline basic_tribool<Type> operator || (basic_tribool<Type> other)
    {
        return traits_type::disjunction(value, other.value);
    }

private:
    typename traits_type::value_type value;
};

// Implementation of Kleene tribool

template <>
struct basic_tribool_traits<basic_tribool_kleene_tag>
{
    enum value_type { false_value, true_value, indeterminate_value };

    static value_type negation(value_type lhs)
    {
        switch (lhs)
        {
        case false_value:
            return true_value;
        case true_value:
            return false_value;
        case indeterminate_value:
            return indeterminate_value;
        }
    }

    static value_type conjunction(value_type lhs, value_type rhs)
    {
        switch (lhs)
        {
        case false_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return false_value;
            case indeterminate_value:
                return false_value;
            }
        case true_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        case indeterminate_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return indeterminate_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        }
    }

    static value_type disjunction(value_type lhs, value_type rhs)
    {
        switch (lhs)
        {
        case false_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        case true_value:
            switch (rhs)
            {
            case false_value:
                return true_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return true_value;
            }
        case indeterminate_value:
            switch (rhs)
            {
            case false_value:
                return indeterminate_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        }
    }
};

typedef basic_tribool<basic_tribool_kleene_tag> tribool;

// Implementation of neutral tribool

template <>
struct basic_tribool_traits<basic_tribool_neutral_tag>
{
    enum value_type { false_value, true_value, indeterminate_value };

    static value_type negation(value_type lhs)
    {
        switch (lhs)
        {
        case false_value:
            return true_value;
        case true_value:
            return false_value;
        case indeterminate_value:
            return indeterminate_value;
        }
    }

    static value_type conjunction(value_type lhs, value_type rhs)
    {
        switch (lhs)
        {
        case false_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return false_value;
            case indeterminate_value:
                return false_value;
            }
        case true_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return true_value;
            }
        case indeterminate_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        }
    }

    static value_type disjunction(value_type lhs, value_type rhs)
    {
        switch (lhs)
        {
        case false_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return false_value;
            }
        case true_value:
            switch (rhs)
            {
            case false_value:
                return true_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return true_value;
            }
        case indeterminate_value:
            switch (rhs)
            {
            case false_value:
                return false_value;
            case true_value:
                return true_value;
            case indeterminate_value:
                return indeterminate_value;
            }
        }
    }
};

typedef basic_tribool<basic_tribool_neutral_tag> neutribool;

}
